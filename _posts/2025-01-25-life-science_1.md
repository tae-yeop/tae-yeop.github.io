---
title:  "신약개발을 위한 생명 과학 기초내용"
excerpt:  ""
categories: 
- Drug discovery

tags:
- Drug discovery
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-25
---


먼저 생명과학 사전 지식

# 기본 화학 지식
- 화학은 분자, 원자간의 원리를 기술함
## 크기, 무게 감각
달톤(Da)
- **수소 원자**: 1 Da
- **물 분자**: 약 18 Da
- **아미노산**: 약 100-200 Da (각 아미노산의 크기와 종류에 따라 다름)
- **글루코스(포도당)**: 약 180 Da
- **ATP(아데노신 삼인산)**: 약 507 Da
- **인슐린(단백질 호르몬)**: 약 5,800 Da
- **헤모글로빈(산소 운반 단백질)**: 약 64,500 Da
- **DNA 염기쌍(단일 염기쌍 기준)**: 약 650 Da

## 화학 결합
### Strong Bonds
- 원자 간의 전자 공유나 전기적 인력
- 1) 공유결합 (Covalent Bond)
    - 1) 극성 공유결합 (Polar Covalent Bond)
    - 2) 비극성 공유결합 (Nonpolar Covalent Bond)
    - 3) 배위 결합 (Coordination Bond)
    - 일반적으로 비금속 원자들 사이에서
    - 물(H₂O), 이산화탄소(CO₂), 메탄(CH₄)


![https://www.youtube.com/watch?v=RF_fW7Hlh6s](https://github.com/user-attachments/assets/13e19f3e-3b89-45b4-9b23-9c9eb0c6da5b)

- 2) 이온결합 (Ionic Bond)
    - 완전 이온화 vs 부분 이온성
    - 전자가 완전히 이동
    - 일반적으로 금속 원자와 비금속 원자 사이에서
    - 높은 녹는점과 끓는점
    - 물에 잘 녹고, 용액에서 전기 전도성
    - 염화나트륨(NaCl), 염화칼슘(CaCl₂)

![Image](https://github.com/user-attachments/assets/2b6eb22e-3424-45e6-8ee8-95035b62a7d9)

- 3) 금속결합 (Metallic Bond)
    - 전기 전도성과 열 전도성이 좋음
### Weak Bonds
- 물학적 상호작용에 중요한 역할
- 1) 수소결합 (Hydrogen Bond)
    - 수소 원자가 산소, 질소, 플루오린 등의 전기음성도가 큰 원자와 결합할 때 형성되는 약한 결합.
    - 다수의 수소 결합은 큰 영향
    - 물의 높은 끓는점, 표면 장력, DNA의 이중 나선 구조 등
- 2) 반데르발스 힘 (Van der Waals Forces)
    - 분산력(London Force) vs 쌍극자-쌍극자 상호작용
    - 분자 간의 약한 상호작용 힘으로, 분자간 인력과 반발력
- 3) 소수성 상호작용 (Hydrophobic Interaction)

# Central Dogma
## DNA
![https://www.youtube.com/watch?v=sWnFFGJyqYk](https://github.com/user-attachments/assets/00e4b48e-1fbe-4318-8a80-eeb61625b1aa)

- DNA : 30억개의 sequence, 진정한 Natural Language
- $5'$에서 $3'$ 방향으로 합성이 이루어짐
    - 프라임 : 분자 내 탄소 원자의 번호
    - 5 프라임 탄소 : 5번 탄소에 인산기 연결, DNA의 시작점
    - 3 프라임 탄소 : 3번 탄소에서 하이드록실기(-OH) 연결, DNA 끝점
    - 하나의 가닥이 구성될 때 5' 인산기와 3' 하이드록실기가 인산다이에스터 결합 화학(탈수 반응)
    - 1 프라임 탄소에 염기가 붙어있음
- Codon : DNA의 3개의 nucleic acids 조합
- Central Dogma : DNA → RNA → Protein (1 Codon $\to$ 1 Amino acide)
- 일부 코돈들은 같은 아미노산을 만드는 중복 현상 (이유는 모름)
- 양 가닥은 수소 결합으로 연결
- DNA는 4개의 단어로 되어 4개에서 몇개씩 엮어서 새로운 token을 만들기도 한다 : ATC, AGT ,… ⇒ 이를 subword라고 함

![Image](https://github.com/user-attachments/assets/b5dfecad-740c-4646-aca2-d89599b8f245)

## RNA

- RNA 중합효소가 DNA 중합효소보다 오류수정 능력이 낮아서 돌연변이가 많이 일어남
## Protein
- 20가지 아미노산 ⇒ 3D 구조를 만듬

![Image](https://github.com/user-attachments/assets/3572753f-1646-43f2-bc85-aeaee11e2f2e)
- 백본은 모든 같은 구조
- R(sidechain, 잔기, 측쇄) + Amino + Hydro + Carbo의 조합
- 고세균, 미생물의 특수 경우를 제외하곤 20개 표준 아미노산

![Image](https://github.com/user-attachments/assets/6d38bbe6-2e6d-4c35-8e99-cec9c43ebda6)
- 특정 R은 Polar Moment(Dipole Moment), Charge 등의 특성을 가짐
- 하이드록실기(-OH)가 있는 경우
    - 산소(O) : 부분적으로 음전하(δ-)
    - 산소는 전기음성도가 높아서 전자를 더 많이 끌어당김 ⇒ 음전하
    - 수소 : 부분적으로 양전하(δ+)



![Image](https://github.com/user-attachments/assets/31888090-edcf-40ee-a839-d867ad822010)
- 1차구조 (Primary Structure)
    - 아미노산 서열, 1D 차
- 2차구조 (Secondary)
    - 국소 배열
    - 아미노산들이 모여서 정형화된 구조를 만듬
    - 정형화 되지 않은 것은 루프라고 부름
    - alpha helix(알파 나선), beta pleated sheet(베타 병풍) :  자주 목격되는 main local building block
    - loop : neither alpha-helix nor beta-sheet (연결부나 굴곡부 같은 다양한 형태)
- 3차구조
    - 2차 구조 (하나의 서열)이 이루는 온전한 접힘 구조
    - 3차원 구조, 이게 흔히 말하는 단백질
    - 폴리펩타이드의 전체 3차원 구조
- 4차 구조
    - 서열 여러개가 뭉치는 구조 (상호작용에 의해)
    - 독립된 단백질의 뭉침
    - 여러 폴리펩타이드 사슬이 결합한 구조


![Image](https://github.com/user-attachments/assets/dad2a28f-582c-4ad0-ab78-ce567a23c84b)

- 펩타이드 결합
    - 아미노산 2~50개 정도
    - signaling molecules, hormones으로 동작
    - COO-와 NH3+가 만나서 H20가 나오고 남은 부분이 결합한다
- 폴리 펩타이드
    - 아미노산이 50개 이상 체인
    - 3차원 구조로 접혀서 functional proteins이 될 수 있음
- 단백질
    - 폴리 펩타이드 여러개가 배열되서 만들어짐


## 결합의 회전
- 펩타이드 결합(C-N)은 부분적인 이중결합 성격(sp2 혼성)을 띠어서 평면 구조 -> 회전이 거의 불가능
- 단백질 접힘은 두 개의 회전 가능한 결합각(Dihedral angle)에 의해 결정됨

![Image](https://www.researchgate.net/profile/Mohammad-Chahkandi/publication/260184022/figure/fig2/AS:667834392772613@1536235535241/Protein-backbone-dihedral-angles-and-22.ppm)
- φ(phi)각
    - N-C(α)와 C(α)-C 사이의 회전을 나타내는 각도
- ψ(psi)각
    - C(α)-C와 C-N(다음 아미노산의 N) 사이의 회전을 나타내는 각도
- 측쇄(곁사슬)의 회전각(χ각)
    - 사이드체인에도 특정 부분에서 자유롭게 회전할 수 있는 결합
- dihedral angle에 의해서 enery state가 변화 ⇒ 구조의 변화 야기


Ramachandran Plot 
- 각 아미노산이 가질 수 있는 φ(phi)각과 ψ(psi)각의 조합을 x축(φ), y축(ψ)으로 놓고 표시
- 색상이 진한곳일 수록 많은 분포
- 흰색은 금기되는 부분
- steric hinderance (입체 장애)로 인해 특정 조합이 선호된다
- 이를 통해 beta-sheet과 alpha-helix가 대부분임을 표현할 수 있다
![Image](https://media.geeksforgeeks.org/wp-content/uploads/20221028131103/Theramchandranplot.jpg)


단백질 역할
- 어떤 3D 구조를 가지느냐 ⇒ 역할 결정
- 구조적 역할
- 신호 전달
- 면역 반응

- 드 노보 단백질(de novo protein)
    - 완전히 새롭게 설계하거나 합성한 단백질
- 오르판 단백질(orphan protein)
    - 두 가지 뜻 중 하나
    - 기능이 알려지지 않은 단백질
        - 유전체(genome) 해독 등으로 서열이 밝혀졌지만, 아직 기능이나 작용 기전이 분명하지 않은 단백질
    - 오르판 수용체(orphan receptor)
        - ‘오르판 GPCR’(orphan G-단백질 결합 수용체)처럼 내인성 리간드(작용 물질)가 아직 밝혀지지 않은 수용체 단백질을 의미
        - 수용체의 구조나 존재는 알지만, 어떤 물질이 결합해 작용을 일으키는지는 모르는 경우 ‘orphan’

# 세포 주요기관
리소좀
![Image](https://github.com/user-attachments/assets/b831f090-ec3b-4e61-ad7b-0ffcbccbfa19)


# 면역 반응

- 선천성, 후천성 면역
- dendritic cell같은 APCs가 항원을 제시함
    - 항원을 가진 녀석을 포식 후 MHC 분자와 결합하여 표면에 항원을 제시함
    - T세포, B세포는 이것을 보고 반응
    - T세포 : 사이토카인 방출 + 독성 물질 분비
    - B 세포 : 항체 분비

- 항체 : IgGAMED

# 단백질 상호작용


단백질-단백질 도킹
- 단백질간의 결합 예측
- 신호전달, 활성화에 단백질끼리 결합하는 경우가 많다
단백질 결합시 주요 상호작용
- 소수성 상호작용 (Hydrophobic Interaction)
    - 단백질 주변 물이 있다는 걸 이해해야함
    - 주변의 물로 인해 물을 싫어하는 것끼리 뭉치게 됨
    - 마치 기름과 물이 분리되는 것처럼, 소수성 부분이 모이면 단백질 결합이 안정화
- 전하 상호작용 (Charged Interaction, 쿨롱 상호작용)
    - (+) 전하와 (-) 전하가 서로 끌어당기는 힘이 작용
    - 예를 들어, 자석의 N극과 S극이 서로 끌리는 것과 비슷
- 각 단백질 안에 일어나느 수소 결합은 상호작용에큰 영향이 없다

단백질 복합체 (Protein Complex)
- 둘 이상의 단백질이 결합하여 형성된 구조
- 리보솜(Ribosome) → 여러 개의 단백질과 rRNA가 결합한 거대한 복합체로 단백질을 합성하는 역할
- 신호를 전달하거나, 특정 반응을 활성화 (Activate)
- 특정한 과정에서 일시적으로 약하게 결합했다가 다시 분리
- 단백질 복합체 관련 질병은 nhibitor(억제제)**를 디자인해서 결합을 방해하는 전략 : PPI (Protein-Protein Interaction) Inhibitor
- CDR(complementary determine region) : 3개의 아미노산 체인에 따라 어떤 항원에 바인딩 될지 결정

단백질 복합체의 종류
(1) Homo-oligomer (동종 올리고머)
- 동일한 단백질끼리 결합해서 대칭적인 구조
- 대칭이라는 사실을 이용해서 구조 예측
    - C-Symmetry: 회전 대칭
    - D-Symmetry: 회전 + 거울 대칭
    - Homo-oligomer의 70% 이상이 C-대칭, 20% 이상이 D-대칭
- 예측 방법: Ab initio 도킹
    - 이리저리 여러 방향으로 단백질을 붙여보며 가장 좋은 결합(score가 높은 결합)을 선택
    - score function을 어떻게 디자인할것인가?
(2) Hetero-oligomer (이종 올리고머)
- 서로 다른 단백질이 결합하여 복합체를 형성
- 대칭이 아닐수도 있음
- 템플릿 기반 예측 방법 : 이미 알려진 좋은 복합체 구조(템플릿)를 찾아서 유사한 구조를 예측

고려할 점
- 단백질을 강체로 가정하지만 실제 결합하면 변형이 있을 수 있음
- 모두 고려하기엔 계산량 큼 -> 상대적 위치 (translation, rotation)만 샘플링하여 예측을 수행 (큰 움직임만 고려)


## Protein folding Problem

- `Anfinsen 실험(1950)`
    - denaturation(변성)을 주어도 원본으로 돌아가는 것을 확인한 실험
    - disulfide를 해도 기능과 구조를 하는 것을 확인
    - 열이나 urea를 사용했더니 단백질 접힘이 풀리는 것을 확인
    - 다시 열을 낮추고 용매를 urea에서 물로 교체 ⇒ 원래 효소의 기능을 회복 (구조를 회복)
    - 가역적인 반응이 가능 하다
    - 즉, 서열 그자체만으로 에너지만 낮추면 단백질 구조 결정 ⇒ 단밸직 접힘 현상은 물리, 화학에 의해 일어남
    - 다시 돌아갈 때 원본 구조로 돌아간다 (다른 구조로 가지 않고)

-  `Levinthal paradox(레빈탈의 역설)`
    - 단백질이 취할 수 있는 모든 구조(접힘 상태)를 ‘무작위로’ 전부 시도 -> 짧은 시간에 접히는 것이 불가능할 정도의 ‘천문학적 시간’이 걸린다는 점에서 생기는 모순
- 실제론 아주 짧은 시간(μs~ms)에 특정한 3차원 구조로 접힘 (1초에 $10^14$ 접힘 시도)
- 부분적으로 안정화되는 중간단계(예: 국소적인 알파-나선 또는 베타-병풍 형성)가 생겨나면서 점진적으로 Gibbs free energy가 낮은(안정된) 상태로 수렴하면서 최종 접힘 형태가 나옴


- 샤페론 단백질(chaperone protein)
    - 3차원 구조로 접히도록(폴딩) 돕거나, 이미 접힌 단백질이 변성(denaturation)되어 잘못된 형태로 뭉치는(응집, aggregation) 것을 방지
    - 최종 복합체의 일부로 남지 않고, 단백질의 올바른 구조 형성을 ‘도와준 뒤’ 다시 떨어져 나옵니다(촉매와 유사한 개념)
## 도킹 결과 평가 지표
도킹하는 후보물질을 실험으로 모두 하기엔 한정
검증하기 위해 분자 동역학 시물레이션
80년대 분자역학 : 단백질 구조를 시뮬레이션하게됨
단백질과 화합물 사이의 랭킹 : 에너지로 표현
낮은 에너지 => affinity
F_nat: 실제 결합과 비교했을 때 얼마나 비슷한지?
LRMSD (Ligand RMSD, Root mean sqrt distance): ligand끼리 얼마나 떨어져있는지
IRMSD (Interface RMSD): 단백질 인터페이스(recptor와 ligand사이 결합 부위)만 비교해서 얼마나 유사한지?

## 정보 기반 도킹
![Image](https://github.com/user-attachments/assets/1ab87fa2-6c76-4527-a18c-f901fcabefdc)
- GalaxyHeteromer
    - Hetero-oligomer는 주형 기반 뿐만 아니라 ab initio에도 활용 가능
    - 기본적으로 hetero-dimer 구조체를 예측한다
    - 더 복잡한 구조는 GalaxyHeteromer를 여러번 돌려서 구조를 예측
    - 두 가지 방법으로 템플릿 탐색

- GalaxyHomomer
    - Homo-oligomer를 예측하기 위한 프로그램
    - 주형 기반을 먼저 수행 ⇒ 주형이 있으면 이를 이용
    - 아니면 Ab initio 도킹으로 예측

- Sequence
    - 아미노산 염기서열만 이용
    - 이때 데이터베이스는 DB-Mo, DB-Ho를 사용
- Structure
    - 각 subunit의 구조를 이용해서 서치
    - subunit structure prediction
        - Strucuture가 인풋으로 오면 이 단계가 필요 없다

## 단백질 구조 시각화
UCSF CHIMERA

## 단백질 데이터
- Conatct map
    - 20개의 sequence의 요소들 내의 i, j번째가 실제로 가까울 있는 것을 표현







# Drugs
---
화학의약품
- 여러 화학 물질을 합성하는 화학 공정을 거쳐서 만듬
- 제네릭 : 특허 기간이 끝난 의약품을 본떠서 만듬 제품

바이오의약품
- 생물체 (대장균, 효모, 동물 세포 등) 에서 유래한 원료로 세포 배양, 유전자 재조합같은 생물 공정을 이용
- 부작용이 적고 효과가 뛰어남
- 주로 류마티스 관절염, 당뇨병, 암 등 난치성 질환 치료에 사용
- 바이오 시밀러 (제네릭의 바이오 의약품 버전, 동등생물의약품)
    - 효능을 동일하지만 완전히 같진 않음
    - 살아있는 세포 생산 조건, 정제 방법 다름 ⇒ 안전성, 유효성 측면에서 경미한 변동
    - 바이오신약 개발에 20~30억 달러가 쓰인다면, 바이오시밀러 개발에는 1/10 수준인 1~3억 달러
    - 의약품의 가격 역시 바이오신약(오리지널 바이오의약품) 보다 50~80% 정도 저렴한 수준


<img src="https://github.com/user-attachments/assets/bc4cb0f5-c32f-41f0-9dcf-bd53e791e96f" width="600" />

합성 신약의 규모가 매우 큼 (화학적 합성 가능한 규모가 $10^{60}$인데 ZINC 데이터에도 $7\times 10^8$가 밖에 없다)
하나의 물질이 FDA 승인 받을 때까지 3조원이 든다 ⇒ 더 증가하는 상황


<img src="https://github.com/user-attachments/assets/cc824619-d86e-48bd-8b5c-995e56faf73d" width="600" />


10가지 이상 전문적인 다양한 분야의 시너지가 필요함 ⇒ 신약 개발이 가능한 나라는 15개 정도밖에 안된다

## 개발 과정




<img src="https://github.com/user-attachments/assets/d7eead5b-1822-48a6-bc8b-9c2d7ef5d907" width="600"/>

(1) Hit Compound(활성물질): 연구 초반에 계기를 마련해줌

(2) Lead(선도 물질)
- Hit로 부터 generation, hit와의 차이는 특허성이 있는 모핵이냐 아니냐
- 동물 모형에서 효력을 확보한 시점을 lead compound를 찾았다고 함

(3) Lead optimization
- Candidate(후보 물질)을 찾음
- 시장에서 경쟁력있는 수준의 물질로 발전시킴


Pharmacology (효능평가)

<img src="https://github.com/user-attachments/assets/6336ee8e-6e66-4b48-bf9a-86201a8f89e2" width="600"/>
- PK (Pharmacokinetics, 약동학)





(1) 발견 단계
    - 질병 타겟(제어할 단백질)을 정하고 신약의 후보물질을 도출
    - Target discovery
   


 - Hit screeing : 케미컬을 찾는다 (질병을 제어하는 표적을 알아감)
    - Lead optimization
        - 초기 활성을 지니는 히트를 리드로 발전
        - 해당 표적 단백질을 제어하는데 만족



- 2) 개발 단계 (Pre-clinininc)
    - 안전성과 유효성을 확인하는 임상시험을 실시
    - 임상시험계획(IND)
        - 임상시험을 실시하기 전에는 반드시 허가 당국으로부터 공식적인 심사와 승인을 받는 절차
        - 미국은 FDA(미국 식품의약국)가 승인하는 IND(Investigational New Drug)
        - 유럽은 EMA(유럽 의약품감독국)이 승인하는 CTA(Clinical Trial Application)
        - 안전성 및 유효성 평가가 완료 ⇒ 의뢰자는 30일 이내 IND 승인 여부를 확인

- 3) 1상, 2상, 3상 임상시험 (Clinincal-trials)

- 4) 신약승인신청(NDA)
    - 임상시험을 마치고 의약품을 제조 및 출시할 수 있도록 허가 당국으로부터 공식적으로 승인 받는 절차
    - 미국은 FDA(미국식품의약국)가 승인하는 신약 허가신청(NDA, New Drug Application), 제네릭의약품 허가신청(ANDA: Abbreviated New Drug Application)
    - 유럽은 EMA(유럽의약품감독국)이 승인하는 판매 허가 신청(MAA, Marketing Authorisation Application)
    - 분야별 전문가들에 의해 절차가 진행



## 항암제

### 개요
- 동물실험과 lymphoma patient(림프암 환자)에 투여 ⇒ 완치됨
- 여기서 얻어진 Mustine 물질로 실험 ⇒ 실패
- Mustagen을 개발하여 FDA에서 처음으로 승인된 항암제
- 7년동안 2000개 식물 항암제 찾음 → 25년 동안 500,000개 식물에서 항암제를 찾음 : (Sloan & Kettering 펀딩)
- Chlorambucil (1953), Melphalan (1953), Cyclophosphamide (1957) : 아직도 사용되는 항암제


![Image](https://github.com/user-attachments/assets/c6910878-b988-461f-985a-e9533beff54d)

- 활동도 : 연세가 높아도 활동을 잘하는 사람
- 비용 : 최근에 나온 좋은 약제는 보험이 적용되지 않음


![Image](https://github.com/user-attachments/assets/1943ca78-dbc5-426f-ba97-77573fe49c8e)



- 병기 결정 : Stage (TNM stage)
- T(Tumor): 종양이 얼마나 큰지, 침습을 얼마나 했는지
- N(Node): 종양 주변의 림프 노드까지 병 진행 여부
- M(Metastasis): 전이가 되어있는지 여부

![Image](https://github.com/user-attachments/assets/2fb2bd04-6a61-4fbe-9e1b-bc0201cf61b4)

- 각 암마다 Stage에 따라 Regimen(치료 계획, 치료 요법)을 결정함
    - 대장암의 경우 얼마나 침습되었는지로 평가한다
    - 2기 이상인 경우에는 항암치료가 들어간다
    - 림프절 노드에서 1~3개면 N1, 4개이상이면 N4
    - Standard Treatment (NCCN guideline)
        - 항암 치료를 어떤 순서로 할지에 대한 가이드라인이 있다
        - 국내에는 식약처 가이드라인을 따라야 보험혜택을 받을 수 있다
    - Clinical study
        - 충분한 치료가 없는경우 임상시험을 통해
    - 용량 결정
        - Body surface area (M2) : 키, 몸무게 ⇒ 투여 용량 결정
        - Age, performance status ⇒ 연세가 많은지 누워만 있는 환자라면 10% 투여용량 줄인다
    - 예시
        - FOLFOX regimen
        - FOL = Folinic acid (leucovorin)
        - F = 5-FU (5-fluorouracil)
        - OX = Oxaliplatin
### Chemotherapy의 종류


|요법|목적|설명|
|------|---|---|
|보조 항암화학요법 Adjuvant chemotherapy|Curative(완치) 목적의 Surgery or 방사선 치료 후 재발을 막기 위해서 시행|Breast cancer, Colon cancer(대장암),  Pancreatic cancer(췌장암), 병기에 따라서 하기도 하고 안하기도 한다, 병이 없거나 잔존하고 있을 수 있어서 수행|
|선행 항암화학요법 Neoadjuvant chemotherapy|Curative 목적의 Surgery or 방사선 치료 전에 tumor size를 줄이고, Early metastasis(초기 전이)를 치료하기 위해 시행|Osteosarcoma (뼈암), Larynx cancer(후두암), 암 크기를 줄이면 수술 범위가 줄어든다, 목의 경우 : 수술 범위를 줄여 목소리를 최대한 살린다, 뼈의 경우 : 일부 뼈만 깍아내도록 한다|
|고식적 항암화학요법 Palliative chemotherapy|완치 목적이 아닌 Survival의 증가 또는 증상의 완화를 목적으로 시행하는 항암 치료|대부분의 Stage IV cancer, 정말 반응이 좋은 경우 수술까지 갈수도 있다, 대부분 항암제 약개발이 이를 위해 만들어짐|
|동시 항암 방사선 치료 Concurrent chemo-radiotherapy(CCRT)|항암 치료와 방사선 치료를 함께 투여하여 수술이 불가능한 경우를 가능케 하거나 치료 후 재발율을 낮추거나, 항암 치료를 통해서 방사선 치료 효능을 올리기 위해서| Rectal cancer(직장암) , Head and neck cancer      Glioblastoma, 직장은 항문 바로 위에 있는데 이를 하지 않고 하면 항문 자체를 날려야함|


항암제 투여방법
- Single agent chemotherapy
    - 약제를 하나만 사용
- Combination chemotherapy
    - 조합하는 방법
    - FOLFOX(대장암에 사용) : 5-FU, Leucovorin, Oxaliplatin
    - FOLFIRI(대장암에 사용) : 5-FU, Leucovorin, Irinotecan
    - AC(유방암): Doxorubicin + Cyclophosphamide


### 항암제의 종류


![Image](https://github.com/user-attachments/assets/60fd6fc1-08c3-4550-88bc-f62fdd09ceb3)

- 화학 함암제 : 암세포 뿐 아니라 전신에 작용 ⇒ 부작용
- 표적 항암제 : 암을 유발시키는 원인 물질에 대해서만 공격 ⇒ 부작용 줄임
- 면역 항암제 : 약을 통해 몸의 면역을 활성화 ⇒ 자기 면역세포가 암을 죽이도록 함

![Image](https://github.com/user-attachments/assets/3d1a7e51-ab1d-4861-8bd9-fbbd3d141c7b)

- 1세대 항암제(세포 독성 항암제)
    - 분열하는 모든 세포에 영향을 끼쳐 분열을 억제하는 약물
    - 골수 세포 등 빠르게 분열 및 성장하는 정상세포에도 영향을 끼칠 수 있다는 단점이 있고,
    - 각종 부작용 (메스꺼움과 구토, 설사, 간손상 등)을 유발
    - 특허가 만료되어 다양한 복제약품이 있으며, 사용 용도가 다양하여 현재도 사용 비중이 높음


![Image](https://github.com/user-attachments/assets/7a950251-6e2b-4900-8cb7-abaafd6809eb)

- 알킬화제
    - DNA에 결합하여 DNA의 구조 변화를 통해 암세포의 성장을 억제
    - ex.Cisplatin, Carboplatin, Cyclophosphamide

![Image](https://github.com/user-attachments/assets/d2361dbe-926d-4d39-945e-287bacf28cbe)
- 대사 억제제
    - DNA 복제를 일으키는 물질과 유사한 구조를 지녀, 본래의 물질이 작용을 못하도록 하여 복제를 억제하는 약물
    - ex. 5-FU, Methotrexate
![Image](https://github.com/user-attachments/assets/15654d2c-3eda-4337-a5ba-e673f7648b37)

- 전신 부작용
    - Alopeica(탈모), 머리 모낭세포는 분열이 빠름
    - 구내염(Mucositis) : 구강세포, 빨리 분열하는 곳임 ⇒ 입안이 헐게 된다
    - 혈액세포 감소(hematological toxicity) : 백혈구, 적혈구, 혈소판 등을 만드는 골수세포 역시 분열속도가 빨라 골수억제(myelosuppression)

- 특정 장기·조직에 대한 독성
    - Nephrotoxicity(신장 독성)
        - Cisplatin(시스플라틴)
        -  신장에 부담을 많이 주어 신부전을 일으킬 위험
        - 수액을 많이 줘서 신장을 최대한 보호한다
    - Pulmonary toxicity(폐 독성)
        - 블레오마이신 (Bleomycin)
        - 폐 섬유화
    - Cardiac toxicity(심장 독성)
        - Doxorubicin(독소루비신)
        - 심근 손상을 유발, 심부전이 위험
        - 심장을 보호하는 약제(덱스라조산트)랑 같이 투여
    - Hypersensitivity(과민 반응)
        - Taxol(‘파클리탁셀’ 계열), Bleomycin
        - 알레르기성 쇼크나 과민 반응

    - Neurotoxicity(신경 독성)
        - Vincristine, Vinblastine, Paclitaxel(‘탁솔’)


![Image](https://github.com/user-attachment s/assets/1a95acd6-c8fb-4e59-82cc-53e74c1d1930)
- CTCAE : 각 부작용에 따라서 단계에 따라서 Grade매긴다
- Critical trial을 할때 CTCAE를 활용한다