

### 성능이 이상하게 나오는 경우

첫번쨰 살필 것은 데이터
데이터 전처리가 제대로 되어 있는지 보자
예를 들어 받은 데이터의 범위가 [0,1]인데 [0, 255]의 단위로 Normalization을 한 경우 accuracy가 매우 떨어짐
CIFAR10의 경우 Mean : [0.49139968  0.48215841  0.44653091]
Std : [0.24703223  0.24348513  0.26158784]으로 해야함
```python
class CIFAR10DataModule(LightningDataModule):
  def __init__(self, args):
    super().__init__()
    self.data_dir = args.data_dir
    self.batch_size = args.batch_size
    self.num_workers = args.num_workers

    self.train_transform = transforms.Compose([transforms.RandomCrop(32, padding=4),
                                          transforms.RandomHorizontalFlip(),
                                          transforms.ToTensor(),
                                          transforms.Normalize((125.3, 123.0, 113.9),(63.0, 62.1, 66.7))])
    self.test_transform = transforms.Compose([transforms.ToTensor(),
                                              transforms.Normalize((125.3, 123.0, 113.9),(63.0, 62.1, 66.7))])

```