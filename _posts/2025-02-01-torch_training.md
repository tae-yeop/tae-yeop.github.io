
# 데이터

## 오픈 데이터 구하기
### 구글 드라이브 다운
- `gdown` 을 pip install하여 다운받을 수 있지만 다운 받는 용량이 제한되었던걸로 기억
- 기본 리눅스 명령어로 다운 받으려면 다음과 같이
- [출처](https://gist.github.com/tanaikech/f0f2d122e05bf5f971611258c22c110f)
```python
curl -L "https://drive.usercontent.google.com/download?id={fileId}&confirm=xxx" -o filename

wget "https://drive.usercontent.google.com/download?id=0B7qZV3T3041pTDMtN09pbklvdm8&export=download&confirm"
```


### 바이두 다운받기
- 중국 연구들을 보면 데이터셋을 하필이면 바이두에 올려 놓는 경우가 많다
- 휴대폰 정보를 넣어서 바이두에 가입했어야 했던거 같은데 그런 과정이 싫은 경우
- motrix라는 


### 데이터 생성하기
- 생성모델로 데이터를 만드는 경우
- seed를 잘 설정하도록 하자
- 파일 무결성 확인하자 : 병렬로 대량으로 만들어서 저장하면 이미지가 깨진 상태로 저장되어 나중에 이 데이터로 인해 오류가 나기도 함



# 파이토치 데이터로더


## DataLoader 클래스

### collate_fn
- 배칭을 하면서 torch.tensor로 바꿔주는 함수
- 디폴트 처리방식은 데이터 차원이 모두 같다고 가정함
- 시퀀스 데이터처럼 길이가 가변적인 경우 그냥 하면 에러남
```python


nlp_data = [
    {'tokenized_input': [1, 4, 5, 9, 3, 2],
     'label':0},
    {'tokenized_input': [1, 7, 3, 14, 48, 7, 23, 154, 2],
     'label':0},
    {'tokenized_input': [1, 30, 67, 117, 21, 15, 2],
     'label':1},
    {'tokenized_input': [1, 17, 2],
     'label':0},
]

loader = DataLoader(nlp_data, batch_size=2, shuffle=False)
batch = next(iter(loader))
>>>
/usr/local/lib/python3.7/dist-packages/torch/utils/data/_utils/collate.py in default_collate(batch)
     80         elem_size = len(next(it))
     81         if not all(len(elem) == elem_size for elem in it):
---> 82             raise RuntimeError('each element in list of batch should be of equal size')
     83         transposed = zip(*batch)
     84         return [default_collate(samples) for samples in transposed]
RuntimeError: each element in list of batch should be of equal size
```
- 미니배치마다 최대 길이 가진 데이터가 다르므로 다이나믹 패딩 필요
- collate_fn의 입력은 `__getitem__`의 리턴값임
- 리턴은 dict, list, tuple 등으로 구성 가능 -> 나중에 data loader 루핑 돌릴때 각각에 대응되는 방식으로 조회하면 됨



# 학습 코드


### 재현성과 결정성
- seed 고정
- 보통 torch, numpy 쪽만 고정해주면 됨
- sklearn 등 과학 계산 라이브러리는 numpy를 내부적으로 쓰므로 numpy 고정필요
- `random` 패키지는 직접 쓰지 않는한 딱히 영향미치는 곳이 없음


## Precision
- bf16
     - FP16 MP와 비슷하지만 float32의 dynamic range를 유지해준다.
     - 메모리를 절반만 사용하여 throughput과 메모리 사용 효율을 높힌다.
     - CPU, GPU 모두에 torch.bloat16을 사용할 수 있다.
     - 기존의 fp16 학습은 안정화를 위해서 GradScaler()같은 추가적인 코드가 들어갔는데 bfloat16은 그런 추가 코드가 필요없다. 

# 분산 학습 
- 핵심은 여러개의 장비를 통한 병렬처리를 하는 것
- 이 분야만 아예 연구하시는 팀도 있음
- 자세히 파보는게 아니면 이미 구현된 라이브러리만 잘 활용해서 가치를 만드는 것에 집중하는게 나음


## Data Parallelism



## Optimizer
- list of dict로 줘도 된다.
```python
optimizer = optim.AdamW([{}, {}, {} ])
for i, param_group in enumerate(optimizer.param_groups):
     print(f"Parameter group {i}: lr = {param_group['lr']}")
```



## 기타 메모리 줄이는 팁

### Activation Checkpoint


### Gradient Accumulation Trick
- 미니배치 한번 뽑고 forward-backward 하는게 아니라 backward를 잠시 멈추고 미니배치를 여러 번 forward 시켜서 축적한 뒤에 backward를 하자.
- 즉 원래 미니 배치 사이즈가 32이고 accmulation step에 2라면 16개씩 미니배치를 forward 넣어 축적을 시킴


## 기타 고려사항
- num_workers : 사용하는 GPU의 4를 곱한 수를 추천
- Pin memory : 메모리를 미리 예약한다는 뜻, CPU가 GPU로 전송하는 속도가 빨라진다

# 라이브러리
## 라이트닝
- 두 가지를 신경쓰면 됨 : Trainer, LightningModule
- LightningDataModule도 데이터셋을 래핑할 수 있는데 괜히 복잡해지니 신경쓰지 말자

다양한 병렬학습을 지원함
잘 안쓰본것도 있는데 안써봐서 확신은 못함
Trainer 옵션을 어떻게 설정하느냐가 중요
- 디폴트인것
     - use_distributed_sampler : 샘플러를 분산 처리해주는것
     - sync_batchnorm=True : 배치 사이즈가 작을 때 신경쓰기
- DistributedDataParallel 2 (strategy='ddp2') = DP in a machine, DDP across machines
- Horovod (strategy='horovod') (multi-machine, multi-gpu, configured at runtime)
- Bagua (strategy='bagua') (multiple-gpus across many machines with advanced training algorithms)


LightningModule

`__init__`
- self.save_hyperameters() 메소드 : __init__의 파라미터로 들어온 값들을 저장해둘 수 있음 
```python
class LitMNIST(LightningModule):
    def __init__(self, conf: Optional[Union[Dict, Namespace, DictConfig]] = None, **kwargs):
        super().__init__()
        # save the config and any extra arguments
        self.save_hyperparameters(conf)
        self.save_hyperparameters(kwargs)

        self.layer_1 = nn.Linear(28 * 28, self.hparams.layer_1_dim)
        self.layer_2 = nn.Linear(self.hparams.layer_1_dim, self.hparams.layer_2_dim)
        self.layer_3 = nn.Linear(self.hparams.layer_2_dim, 10)


conf = {...}
# OR
# conf = parser.parse_args()
# OR
# conf = OmegaConf.create(...)
model = LitMNIST(conf=conf, anything=10)

# Now possible to access any stored variables from hparams
model.hparams.anything

# for this to work, you need to access with `self.hparams.layer_1_dim`, not `conf.layer_1_dim`
model = LitMNIST.load_from_checkpoint(PATH)
```


- validation 도 다중 프로세스 싱크해주는 기능을 있음 : self.log에 sync_dist=True
```python
def validation_step(self, batch, batch_idx):
    x, y = batch
    logits = self(x)
    loss = self.loss(logits, y)
    # Add sync_dist=True to sync logging across all GPU workers (may have performance impact)
    self.log("validation_loss", loss, on_step=True, on_epoch=True, sync_dist=True)


def test_step(self, batch, batch_idx):
    x, y = batch
    logits = self(x)
    loss = self.loss(logits, y)
    # Add sync_dist=True to sync logging across all GPU workers (may have performance impact)
    self.log("test_loss", loss, on_step=True, on_epoch=True, sync_dist=True)
```


`forward`
- clip이나 lpips 처럼 추론만 forward에 필요한 경우
     - forward에서 eval()을 수동으로 넣어줌 (안그러면 train() 자동으로 걸렸던걸로 기억)
     - freeze(), unfreeze()를 통해 grad 안 넘길수 있었던걸로 기억

최적화
```python
Trainer(profile=True)

# or

profiler = AdvancedProfiler()
Trainer(profiler=profiler)
```

[재현성](https://github.com/Lightning-AI/lightning/blob/master/src/lightning/fabric/utilities/seed.py)
```python
from pytorch_lightning import Trainer, seed_everything

seed_everything(42, workers=True)
# sets seeds for numpy, torch, python.random and PYTHONHASHSEED.
model = Model()
trainer = Trainer(deterministic=True)
```


구버전 vs 신버전
- 1.5 버전에선 toggle_optimizer()을 할때 optimizer_idx가 인자로 들어가야 함
```python
TypeError: toggle_optimizer() missing 1 required positional argument: 'optimizer_idx'
```


## 라이트닝 패브릭
- 라이트닝에 비해 저수준 API
- 고수준으로 지원하지 않는 기능이 많음
     - grad accmulation
     - sync batch
     