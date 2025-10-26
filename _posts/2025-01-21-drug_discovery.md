

## 라벨
- 데이터에서 다음 상수값들을 라벨링으로 쓸 수 있다.
- 결합 친화도가 높은 화합물은 더 낮은 농도로도 단백질과 강하게 결합하여 기능을 저해할 수 있음

| Constant | Definition | Meaning | Characteristic |
|----------|-----------|---------|---------------|
| Ki | Enzyme-inhibitor dissociation (타겟 분자가 일반적인 단백질이 아닌 효소에 특정하여), 단백질-화합물 상호작용을 측정 | Inhibitor binding strength | Concentration-independent |
| Kd | Ligand-receptor dissociation, 해리 상수 (dissociation constant) | Ligand-receptor affinity | Concentration-independent |
| IC50 | 50% inhibition concentration (물리적인 바인딩이 아니라 phenotype에 대한 기능을 측정), 타깃(단백질, 암세포 혹은 병원균)을 최대 50% 억제할 수 있는 약물 농도 | Inhibitor potency | Concentration-dependent |
| EC50 | 50% max response concentration | Agonist potency | Concentration-dependent |


- IC50와 Ki값은 분리해서 사용하는게 추천된다
- IC50가 가장 고품질의 데이터 ← 우선 사용
- Ki, Kd는 의미가 다르지만 합쳐서 사용하는 경우가 있다 ← 차선책



### IC50(반최대억제농도, Half maximal inhibitory concentration)
- 특정 생물학적 또는 생화학적 기능을 억제하는 물질의 효능을 측정하는 값 
- a measure of the potency of a substance in inhibiting a specific biological or biochemical function
- 특정 생물학적 과정이나 생물학적 구성 요소를 50% 억제하는 데 필요한 양을 나타내는 정량적 지표
- IC50 값은 나노몰(nM)에서 마이크로몰(μM) 범위
- pIC50 : IC50에 log
$$
    \text{pIC}_{50} = -\log_{10}\left(\frac{\text{IC}_{50} \, \text{(in nM)}}{10^9}\right) = 9 - \log_{10}(\text{IC}_{50}\, \text{(in nM)})
$$
- 값의 범위를 줄여서 범위를 좀 더 균등하게 함
- nM 나노몰 : 1리터(1L) 당 10⁻⁹ 몰(mol)의 농도
- pIC50 높은 값 ⇒ 해당 물질이 더 강하게 결합하는 것을 의미

### Lipinski's Rule of Five (Drug-likeness)
- 경구용 약물로서의 적합성을 평가하는 데 사용되는 경험적 가이드라인
- **1. 분자량(Molecular Weight)**
    - 약물의 분자량이 500 달톤(Da)을 넘지 않게

- **2. LogP (지용성/수용성의 비율)**
    - logP 값(지용성과 수용성의 비율)이 5를 넘지 않아야
    - 이 값은 약물의 지용성 여부
    - **logP = 0**: 물과 지방 사이에서 동일하게 분포
    - **logP < 0**: 물에 잘 녹고(수용성), 지방에는 잘 녹지 않음(지용성 낮음)
    - **logP > 0**:  값이 높으면 약물이 세포막(지질 이중층)을 통과하는 데 유리
    - 지나친 지용성 ⇒ 물과 같은 체액에 녹지 않음 ⇒ 생체 내 이동이 어려움 + 또한 독성이나 약물 대사 문제 유발

- **3. 수소 결합 공여기(Hydrogen Bond Donors)**
    - 수소 결합을 제공할 수 있는 공여기(수소 결합 공여 원자, 보통 OH나 NH 그룹)의 수가 5개 이하
    - 갯수 많음 ⇒ 물에 잘 녹을 가능성 상승
    - 지나치게 많음 ⇒ 분자의 지용성을 감소 ⇒ 세포막 통과 힘듬
    - 지나치게 많음 ⇒ 다른 분자와 강한 상호작용 ⇒ 체내 대사 분해 ⇒ 약물 안전성 낮아짐

- **4. 수소 결합 수락기(Hydrogen Bond Acceptors)**
    - 수소 결합을 수용할 수 있는 수락기(주로 산소와 질소 원자)의 수가 10개 이하
    - 수소 결합을 형성할 수 있는 전자쌍을 가진 원자, 주로 산소(O)나 질소(N)와 같은 전기음성도가 높은 원자들을 의미
    - 수소 결합 수락기가 많음 ⇒ 분자 극성 증가 ⇒ 수용성 높아짐 ⇒ 너무 많으면 세포막 통과 어려움
    - 경구로 투여된 약물 ⇒ 소화관에서 흡수 ⇒ 혈류를 통해 표적 부위로 이동


### ADME
- 흡수 (Absorption)
    - 생체 이용률(Bioavailability)
    - 전신 순환에 도달하는 비율
    - 100%에 가까울수록 흡수
    - F값은 경구 투여된 약물의 혈중 농도 곡선(AUC)과 정맥 투여된 약물의 AUC를 비교하여 계산

- 분포 (Distribution)
    - 분포 용적(Volume of Distribution, Vd)
    - 약물이 체내에서 어떻게 분포되는지를 나타내는 지표
    - 얼마나 널리 퍼지는지를 평가
    - 약물이 특정 조직에 대한 친화성이 높은 경우 Vd 값이 높게 나옴

- 대사 (Metabolism)
    - 클리어런스(Clearance, CL)
    - 빨리 대사되거나 제거되는지
    - 간 클리어런스(CL_hepatic), 신장 클리어런스(CL_renal) 등이 있으며, CL 값이 높으면 약물이 빠르게 제거됨을 의미

- 배설 (Excretion)
    - **반감기(Half-life, t1/2)**
    - 농도가 절반으로 감소하는 데 걸리는 시간
    - 약물의 지속성을 평가

## Feature
- 기본 피처: 극성, 분자 weight, atom 수 등등
- 2D : SMILES, InChI
- 3D : PDB, SDF
- 1D : Fingerprint
- 2D : Fingerprint
- 3D : Fingerprint
- 3D : Conformation
- 3D : Docking
- 3D : Molecular Dynamics
- 3D : Quantum Chemistry
- 3D : Quantum Mechanics
- 3D : Quantum Mechanics/Molecular Mechanics
- 3D : Quantum Mechanics/Molecular Mechanics/Generalized Born
- 3D : Quantum Mechanics/Molecular Mechanics/Poisson-Boltzmann
- 3D : Quantum Mechanics/Molecular Mechanics/Poisson-Boltzmann/Generalized Born

![Image](https://github.com/user-attachments/assets/fd164982-950c-4dcd-9bd1-8e7cc6c6b74d)
SMILES의 경우 DFS를 통해 하나씩 표기함



(1) ECFP
(2) MACCS



# 분자 데이터 처리
## 시퀀스 표현
- 문자열로 표현되서 NLP 비슷하다고 보면 됨
### SMILES notation
![Image](https://github.com/user-attachments/assets/0b3838a3-2283-49c0-9898-7d8a76078806)

![Image](https://github.com/user-attachments/assets/47207754-c098-47f2-a355-1bad8f20fa3f)

![Image](https://github.com/user-attachments/assets/23bb821d-8cbc-49c3-8600-0627ee6077d0)

![Image](https://github.com/user-attachments/assets/2e06e4dc-1ddb-45a8-bd98-18d5616de5c9)

![Image](https://github.com/user-attachments/assets/81b5582e-d468-4170-9ee6-d48f26258c7e)

![Image](https://github.com/user-attachments/assets/80ca8f2a-0264-4aed-8b9d-0185c292c678)

![Image](https://github.com/user-attachments/assets/5be8b05c-9eab-4feb-b4cd-f03589b5b67b)

![Image](https://github.com/user-attachments/assets/b325bafe-02a8-4c97-81eb-df1040aecad7)

![Image](https://github.com/user-attachments/assets/d9b55652-d38a-493a-84d0-906cde05c98e)

![Image](https://github.com/user-attachments/assets/51fb39d7-29fb-4b9b-b0ac-8da973138e8a)

![Image](https://github.com/user-attachments/assets/ec972e68-8d43-4ff4-a45c-9f83f8bb8681)

![Image](https://github.com/user-attachments/assets/a7dd9845-f5e6-42fb-99b0-1d278db76acd)

![Image](https://github.com/user-attachments/assets/0ee2d97d-15e0-40b5-8381-e6895b7b0fc7)

![Image](https://github.com/user-attachments/assets/b2d01c24-0c93-47c7-945e-120fcdc38c27)

![Image](https://github.com/user-attachments/assets/01bf9b3e-b0d8-4048-8d50-cdeafd1b3f43)

![Image](https://github.com/user-attachments/assets/34f498f0-8499-40c3-aa07-ba70f6613f31)


### InChI notation (인치키)
![Image](https://github.com/user-attachments/assets/801f59e0-44c7-4bb9-9dfd-99a5ea00c8a3)
- SMILES는 한 분자를 여러 표현으로 나타내버림
- 유니크한 표현을 위해서 IUPAC에서 만든 노테이션
- 더 많은 표현을 할 수 있지만 읽기 힘들다
- SMILES 보다 인기가 없다


\n : 엔드코돈
### Molecular Descriptor
- 분자구조를 수학적으로 해석하여 도출한 값

![Image](https://github.com/user-attachments/assets/f4dedeed-be28-4a03-b0a4-9a43abb821ea)

![Image](https://github.com/user-attachments/assets/b89bc745-7771-4769-bfcd-d8ef68611b16)


천연물의 경우
NC-MFP
천연물에 특화된 분자지문
 1) scaffold
 2) fragment (주변 조각)
천ㄴ연물의 코어 구조를 표현할 수 있다고 함

분자지문의 길이는 고정 (동일한 차원 길이의 임베딩이라고 생각)


Modered의 경우
문자처리르 고려하게끔 할 수 있다 : remove-processing
문자가 나오면 0ㅇ로 치환:  replace-processing
Padel : Modered 이전 feature 얻는 기법

## 위상 표현
Tanimoto Similarity

- 두 분자의 지문(Fingerprint) 표현자 간의 유사성을 계산하는 방법

Tanimoto Similarity=A∪BA∩B

여기서 A∩BA \cap BA∩B는 두 벡터의 교집합(둘 다 1인

여기서

A∩BA \cap B

A∩B는 두 벡터의 교집합(둘 다 1인 경우의 수),

A∪BA \cup B

A∪B는 두 벡터의 합집합(적어도 하나가 1인 경우의 수)입니다.

a. a=[0,0,0,1]a = [0,0,0,1]a=[0,0,0,1], b=[0,0,0,1]b = [0,0,0,1]b=[0,0,0,1]

- A∩B=1A \cap B = 1A∩B=1
- A∪B=1A \cup B = 1A∪B=1
- Tanimoto Similarity = 11=1
    
    11=1\frac{1}{1} = 1
    

b. a=[1,1,1,1]a = [1,1,1,1]a=[1,1,1,1], b=[0,1,0,1]b = [0,1,0,1]b=[0,1,0,1]

- A∩B=2A \cap B = 2A∩B=2 (1,1 and 1,1)
- A∪B=4A \cup B = 4A∪B=4
- Tanimoto Similarity = 42=0.5
    
    24=0.5\frac{2}{4} = 0.5
    

c. a=[1,0,0,0]a = [1,0,0,0]a=[1,0,0,0], b=[0,0,0,1]b = [0,0,0,1]b=[0,0,0,1]

- A∩B=0A \cap B = 0A∩B=0
- A∪B=2A \cup B = 2A∪B=2
- Tanimoto Similarity = 20=0
    
    02=0\frac{0}{2} = 0
    

d. a=[1,1,1,0]a = [1,1,1,0]a=[1,1,1,0], b=[0,1,1,1]b = [0,1,1,1]b=[0,1,1,1]

- A∩B=2A \cap B = 2A∩B=2 (1,1 and 1,1)
- A∪B=4A \cup B = 4A∪B=4
- Tanimoto Similarity = 42=0.5
    
    24=0.5\frac{2}{4} = 0.5
    

따라서, Tanimoto Similarity가 가장 큰 경우는 a입니다.

정답: a. a=[0,0,0,1]a = [0,0,0,1]a=[0,0,0,1], b=[0,0,0,1]b = [0,0,0,1]b=[0,0,0,1]


## 그래프 표현
- 분자를 string으로 다루는건 부족하다.
- 사람이 분자를 다루는 방식은 sequence가 아니다 ⇒ AI도 그래프로 하는게 좋지 않을까
- 실제론 메틸기(작용기)만 차이가 있지만 SMILES string상에선 완전히 다르게 보인다. ⇒ VAE는 다른 latent space에 매핑할 확률이 높다 ⇒ 학습 난이도가 높다.



### Conatct map
- 20개의 sequence의 요소들 내의 i, j번째가 실제로 가까울 있는 것을 표현

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

# 설치 확인
python -c "from rdkit import Chem; print(Chem.MolToMolBlock(Chem.MolFromSmiles('C1CCC1')))"
```
- rdkit.Chem : 많이 쓰는 함수가 들어 있음
- rdkit.Chem.AllChem : 좀 더 고급 기능, 덜 쓰는

### Remarks
- 같은 분자라도 다른 SMILES 표현이 있을 수 있음




# Task

DTI
- Drug Target Interaction
- 화합물이 표적단백질과 상호작용해서 기능을 제어하는 것을 말함
- 구성 요소
    - 리간드(ligand) : 큰 분자와 결합하는 작은 분자
    - 활성부위(binding site) : 화합물이 결합하여 생물학적 효과를 발휘하는 부위
- 두 가지 방식
    - docking-based
        - 단백질과 리간드 모델에 대해서 3차원 구조로 상호작용
        - 에너지 레벨을 통해 판단
        - 사람이 이해하기 쉽다
        - 3차원 정보를 가지고 있어야 이해할 수 있다
        - 제한된 수의 단백질들만이 3차원 구조를 가지고 있다

    - machine-learning-based
        - drung, protein descriptor를 활용 (구조 정보, 아미노산 조성 정보 등)
        - 3차원 구조 정보없이도 예측 가능
        - Protein에 ligand가 어떻게 도킹하는지 해석이 힘들다

- DTI matrix를 구축할 수 있다
- 이를 활용해 잠재 약물을 찾는다

PPI

Protein Structure


## DTI(Drug target interaction)
- 화합물이 표적단백질과 상호작용해서 기능을 제어

## PPI(Protein-Protein Interaction)
- 단백질의 주변 환경 이해가 필수:
    - 소수성 상호작용 (Hydrophobic Interaction): 물을 싫어하는 분자끼리 뭉침.
    - 전하 상호작용 (Charged Interaction): 쿨롱 법칙에 따른 정전기적 인력.





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


### Classic ML methods for
바이오 데이터는 갯수가 적어서 전통적인 머신러닝 기법을 하는게 좋을 수 있다
- Random forest : Decision Tree의 앙상블
- SVM : Hyperplane을 예측해서 이를 decision boundary로 씀
- 쓸만한 라이브러리 : sklearn, xgboost, lightgbm, catboost


### 가상 스크리닝
- 특정 단백질과 반응하는 분자를 예측
- 결합 가능성, 대사 배출 등을 통해 리간드를 발굴

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

- Multi-modal pre-training
    - Label 되지 않은 많은 데이터 => 이것들을 활용하여, 사전에 좋은 embedding을 얻기
    - 분자는 Graph, SMILES 두 가지로 표현
    - 이외에도 분다를 SMILES, IUPAC으로도 표현 (Multi-lingual 이라고 생각할 수 있음) (Multilingual Molercular Representation learning via Contrastive Pre-training)

![Image](https://github.com/user-attachments/assets/91355ce0-9b2a-466d-9646-a32776dcf43b)

![Image](https://github.com/user-attachments/assets/0522eca5-4b3e-4a01-be9f-e743dd97c983)

![Image](https://github.com/user-attachments/assets/109e87ef-088e-41b5-bc88-c147a49fde31)

- 생성 모델 프레임워크 사용


VAE 접근법
- latent space 뿐만 아니라 condition 까지 직접 줄 수 있다 ⇒ 원하는 물성을 갖는 분자를 생성
- 단점
    - Prior을 가정 (분포가 가우시안이라고 가정 ⇒ 실제론 다른 분포일수도 있고 학습이 제대로 안될 수도 있다)
    - SMILES에 대한 최적의 모델은 아닐 수 있다



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


