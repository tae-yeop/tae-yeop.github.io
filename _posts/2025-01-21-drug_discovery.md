

De novo drug design

# 데이터 다루기
## 데이터 소스
- [BindingDB](https://www.bindingdb.org/rwd/bind/)
    - 단백질-화합물 결합 친화도 데이터를 제공하는 데이터베이스이다.
- [PubChem BioAssay](https://pubchem.ncbi.nlm.nih.gov)
    - 화합물의 구조, 생물학적 활성, 독성 및 기타 생물학적 특성에 대한 정보를 제공
- [ChEMBL](https://www.ebi.ac.uk/chembl/)
    - 화합물의 생리적 활성 및 약리학적 정보를 포함
    - 사람이 일일이 바이오 활성을 가지는 화합물에 대한 정보를 DB 구축
    - 2.4M개의 Compounds
    - 1.5M개의 Assays(activity 실험 데이터)
        - binding assay : small molecule과 binding하는지

![Image](https://github.com/user-attachments/assets/10a58e37-8e3f-45fd-b9de-142a13eb763f)

    - CSV를 클릭해서 다운받기
    - 다큐먼트 ID마다 개별적인 실험 환경
    - 일일이 클릭하기 힘들기 때문에 API를 제공한다
- [ZINC](http://zinc.docking.org/)
- [SciFinder](https://scifinder.cas.org/)
- [Protein Data Bank, PDB](https://www.rcsb.org/)
    - 단백질과 기타 생체 분자의 3차원 구조 정보를 제공하는 데이터베이스이다.
- [Cambridge Crystallographic Data Center](https://www.ccdc.cam.ac.uk/structures)
- [DrugBank]
    - 신약 개발과 관련된 생리활성 화합물의 구조와 생물학적 활성을 포함하는 데이터베이스이다.


## 라벨
- 데이터에서 다음 상수값들을 라벨링으로 쓸 수 있다.

| Constant | Definition | Meaning | Characteristic |
|----------|-----------|---------|---------------|
| Ki | Enzyme-inhibitor dissociation (타겟 분자가 일반적인 단백질이 아닌 효소에 특정하여) | Inhibitor binding strength | Concentration-independent |
| Kd | Ligand-receptor dissociation | Ligand-receptor affinity | Concentration-independent |
| IC50 | 50% inhibition concentration (물리적인 바인딩이 아니라 phenotype에 대한 기능을 측정) | Inhibitor potency | Concentration-dependent |
| EC50 | 50% max response concentration | Agonist potency | Concentration-dependent |

- IC50와 Ki값은 분리해서 사용하는게 추천된다
- IC50가 가장 고품질의 데이터 ← 우선 사용
- Ki, Kd는 의미가 다르지만 합쳐서 사용하는 경우가 있다 ← 차선책



## 데이터 포맷


## RDKit
- 분자 데이터를 다룰 수 있는 라이브러리
- [설치](https://www.rdkit.org/docs/Install.html)

```python
ImportError: libtiff.so.5: cannot open shared object file: No such file or directory

-> 
sudo apt install libtiff5
apt-get install libxrender1
conda create -c conda-forge -n myenv rdkit
```
- rdkit.Chem : 많이 쓰는 함수가 들어 있음
- rdkit.Chem.AllChem : 좀 더 고급 기능, 덜 쓰는


# Task

## 신약 개발
![Image](https://github.com/user-attachments/assets/143d3df0-7e51-4c4a-a87c-1b8046e52555)

![Image](https://github.com/user-attachments/assets/c9a8ecaf-93f1-4e0d-8432-1272e77c7086)

- 후보 물질 발굴 (기초, 탐색 연구, 비임상) → 전임상 → 임상시험
1) 후보물질 발굴

- 약물로 활용될 수 있는 신규 화합물  발굴
- 케미컬 스페이스 : $10^{30}$
- 전체 신약 개발 비용의 33프로가 여기에 소요
- 스크리닝을 통해 평균 10개 정도



### QSAR(Quantitative Structure-Activity Relationship) 모델링

- 화합물의 생물학적 활성을 예측
- 화합물의 구조적 특성과 그 생물학적 활동 사이의 관계를 규명
- 새로운 화합물의 효능을 예측하는 데 사용


# 어떤 AI 방법론이 있을까?


## 생성모델
왜 생성모델을 쓰는가?
- Chemical space($10^{60}$)가 너무 크니깐 이미 있는 Drugs Space 내에서 신약을 찾아내자.


- 시퀀스 데이터 처리 기법
- 바이오 사이언스 데이터는 시퀀스로 이루어진게 많다 -> 시퀀스 처리하는 방법론을 사용하자

- 그래프 표현을 이용
    - 알파폴드 또한 그래프를 Transformer 기반으로
    - Non-euclidean이기 때문에 zero로 채워서 grid shape를 고정하는 방식과는 다르다 
    - 더 일반화되었기 떄문에 모든 데이터를 Graph로 표현할 수 있다
    - 이미지에서도 그래프를 적용하여 structure를 잡아낼 수 있다

- 모달리티를 늘리자
- 분자를 다른 표현으로 : 그래프, SMILES, IUPAC
    - Dual-view Moleclue Pre-training
    - MoCL: Contrastive Learning on Molecular Graphs with Multi-level Domain Knowledge

![Image](https://github.com/user-attachments/assets/91355ce0-9b2a-466d-9646-a32776dcf43b)

![Image](https://github.com/user-attachments/assets/0522eca5-4b3e-4a01-be9f-e743dd97c983)

![Image](https://github.com/user-attachments/assets/109e87ef-088e-41b5-bc88-c147a49fde31)


- 생성 모델 프레임워크 사용


## 시퀀스 
### LLM
- 대표적인게 LLM이다. 
- 주어진 sequence에서 다음 단어의 확률을 예측
- 구현하기 쉬움
- 학습이 쉬움
- 단점은 latent space 분석이 불가능


- 기존의 LLM은 단어에 대해서 동작했는데 어떤 것을 단어로 볼지 정해야함
    - 아미노산 하나를 단어로 볼것인지
    - 아미노산 하나를 캐릭터로 볼 것인지?

단어의 의미는 자연어와 같은지? 다른 방식의 정의가 필요한지?

- 임베딩 벡터로 의미로 표현되겠는가?
- 의미가 무엇일까? 단백질 부위의 역할일까? 상호작용일까?

단어 간의 관계가 단백질에선 어떤 의미인지?

- 아미노산이 만드는 secondary stucture가 단어로 볼 수 있지 않을까
- 여기선 각 아미노산 residue를 보도록 한다.



## 생물학적 도메인 지식
### Co-evolution
- 미오글로빈은 사람, 동물 모두 유사함
- 비둘기와 사람은 전혀 다르지만 단백질을 유사한 부분이 있다

진화를 해오면서 산소를 옮기는 같은 똑같은 역할을 하는 것만 남아서

Co-evolution이 있으면 contact를 하고 있다.

MSA를 언어 모델로 바꾸어도 알파폴드와 그렇게 떨어지지 않는다는 결과가 있다.

Co-evolution은 Attention에 반영된다

참조한 것이 어떻게 연결될지에 대한 정보가 여기에 있어서

Attention map을 모두 concat해서 linear에 넣는다