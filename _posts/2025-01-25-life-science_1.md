---
title:  "Alphafold"
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

## 단백질 데이터
- Conatct map
    - 20개의 sequence의 요소들 내의 i, j번째가 실제로 가까울 있는 것을 표현


## DTI(Drug target interaction)
- 화합물이 표적단백질과 상호작용해서 기능을 제어

## PPI(Protein-Protein Interaction)
- 단백질의 주변 환경 이해가 필수:
    - 소수성 상호작용 (Hydrophobic Interaction): 물을 싫어하는 분자끼리 뭉침.
    - 전하 상호작용 (Charged Interaction): 쿨롱 법칙에 따른 정전기적 인력.



