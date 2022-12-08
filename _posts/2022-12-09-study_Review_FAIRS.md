---
title:  "[Standard] Paper Review : FAIRS 데이터 사용 가이드라인"
excerpt: FAIRS 데이터를 활용해보자"

categories: [Study, Standard, Review]
tags:
  - [의학, 표준, standardization, standard, medicine, FAIRS]

toc: true
toc_sticky: true
 
date: 2022-12-09
last_modified_at: 2022-12-09
math: true
comments : true
mermaid: true
---

# Comment: The FAIR Guiding Principles for scientific data management and stewardship

- Fair Guiding Principle에 대한 Comment들을 다룬 논문
- 개인이 데이터를 재사용할 수 있도록 지원 + 데이터를 자동으로 찾고 사용하는 능력을 향상시키는 데 중점을 둔다

## Supporting discovery through good data management
- 기존의 디지털 생태계는 연구로부터 최대의 이익을 얻는 것을 방해한다
- Data stewardship은 long-term care 개념을 포함하고 있다.
  - 귀중한 데이터 자산을 발견
  - 연구를 위해 새로 생성된 데이터와 함께 재사용될 수 있어야 함
- 그러나 '좋은 데이터 관리'를 구성하는 것은 대부분 정의되지 않았으며 일반적으로 데이터, 리포지토리 소유자의 결정으로 남겨짐.
- 이 논문은 '좋은 데이터 관리'의 목표를 명확히 하고, 권한을 정의하며 학술 데이터를 게시 및 보존하는 사람들에게 알리기 위한 간단한 지침서를 정의하고자 함
  - Findability 발견가능성
  - Accessibility 접근성
  - Interoperability 상호운용성
  - Reusability 재사용가능성
- 이에는 다양한 이해관계자가 존재하고, 이들이 이 원고를 쉽게 읽을 수 있도록 일반적인 약어에 대한 정의를 나열
  - BD2K
    - Big Data To Knowledge.
    - 생물의학 연구, 새로운 지식을 쉽게 발견하고 지원하며, 지역사회 참여를 극대화하기 위해 설립된 trans-NIH initiative
  - DOI
    - Digital Object Identifier
    - 디지털 개체를 영구적, 안정적으로 식별하는 데 사용되는 코드
    - 메타데이터를 검색하기 위한 표준 메커니즘과 일반적으로 데이터 객체 자체에 액세스하는 수단을 제공
  - FAIR
    - Findable, Accessible, Interoperable, Reusable.
  - FORCE11
    - The Future of Research Communications and e-Scholarship
    - 2011년에 시작된 지식 창출과 공유 향상을 위한 변화를 위해 학자, 사서, 기록 보관자, 출판자 및 연구 자금 제공자의 조직적 커뮤니티
  - Interoperability
    - non-cooperate resource data들이 tool로 통합하거나 함께 작업할 수 있는 능력
  - JDDCP 
    - Joint Declaration of Data Citation Principles
    - 데이터를 1등급 연구 결과물로 인정하고 데이터 재사용에 관한 좋은 연구 관행을 지원하기 위해 JDDCP는 학술 문헌, 다른 데이터 세트 또는 기타 연구 객체 내에서 데이터 인용을 위한 일련의 지침 원칙을 제안
  - RDF
    - Resource Description Framework
    - Machine이 읽고 해석할 수 있도록 설계된 데이터 및 지식 표현을 위해 인정받는 프레임워크
- 인간 뿐만 아니라, computational한 이해관계자들도 중요하다.
- 특별한 목표를 지닌 레포지토리가 있다.
  - Life Science
    - Genbank3
    - Worldwide Protein Data Bank (wwPDB4)
    - UniProt5 
  - Space Science
    - Space Physics Data Facility (SPDF; http://spdf.gsfc.nasa.gov/)
    - Set of Identifications
    - Measurements and Bibliography for Astronomical Data (SIMBAD6)
- 기존의 low-throughput bench science에서 나온 많은 데이터셋들은 이러한 특수 목적 저장소의 데이터 모델에 맞지 않지만, 통합 연구와 재현성 및 재사용 측면에서 마찬가지로 중요합니다
  - 다양한 general-purpose data repositories들이 있다.
    - Dataverse7
    - FigShare(http://figshare.com)
    - Dryad8 
    - Mendeley Data(https://data.mendeley.com/)
    - Zenodo(http://zenodo.org/)
    - DataHub (http://datahub.io), 
    - DANS (http://www.dans.knaw.nl/)
    - EUDat9
  - 이러한 데이터 생태계는 좋은 integration에서 멀어지고 있는 것으로 보임 
  - 또한 데이터들이 더 다양해지고 덜 통합되어 인간과 computational agents의 발견 및 재사용성 문제를 악화시키고 있음
- 다음과 같은 것들을 해결하고 싶다
  - 원하는 데이터셋이 존재하는가? 존재한다면 어디에? 
  - 메타데이터들을 어떻게 검색할 수 있는가?
  - 개인이 가진 데이터와 쉽게 통합할 수 있는가?
  - 연구자는 이러한 제3자 연구자의 데이터를 사용할 수 있는 권한을 가지고 있으며, 어떤 라이센스 조건 하에서 사용되어야 하는가?
  - 특정 데이터 포인트를 재사용할 경우 인용되는가?
- 필요한 데이터를 수집하기 위해 몇 주(또는 몇 달)의 전문적인 기술적 노력이 필요한 이유는 적절한 기술의 부족이 아니라, 우리가 귀중한 디지털 물체를 만들고 보존할 때 당연히 해야 할 세심한 주의를 기울이지 않기 때문이다.
- 따라서 이러한 장벽을 극복하려면 연구자, 특수 목적 및 범용 저장소를 포함한 모든 이해 관계자가 위에서 설명한 새로운 과제를 충족하기 위해 진화해야 한다.
- 이를 위해 FAIR가 등장

## The significance of machines in data-rich research environments
- FAIR가 인간 주도 활동과 기계 주도 활동 모두에 적용되는 것에 중점을 두는 것은 다른 peer initiative들과 구분되는 FAIR 지침 원칙이다.
- 인간은 발견 및 통합 작업을 대신 수행하기 위해 computational agent에 점점 더 많이 의존
- machine actionable : 데이터를 탐색하고 제공하는 데 있어서 연속적으로 업데이트됨을 나타내는 표현
  - a) 물체의 유형을 식별한다.
  - b) 메타데이터 및 데이터 요소를 조사하여 agent의 현재 task 내에서 유용한지 여부를 판단한다.
  - c) 라이센스, 동의 또는 기타 접근성 또는 사용 제약조건과 관련하여 사용 가능 여부를 결정한다.
  - d) 인간이 할 수 있는 것과 거의 같은 방식으로 적절한 행동을 취한다.
- 데이터/저장소 수준에서 보다 일반화된 상호운용성 기술 및 표준을 적용하여 데이터를 발견하고 탐색하는 데 있어서, machine들을 assist하는 것이 좋은 데이터 관리를 위한 최우선 과제이다.

## The FAIR Guiding Principles in detail

- FAIR 지침 원칙은 수동 및 자동 증착, 탐색, 공유 및 재사용을 지원하는 것과 관련하여 현대 데이터 게시 환경에 대한 명확한 고려 사항을 설명
- 현대 데이터 리소스, 도구, 어휘 및 인프라가 갖춰야 할 특성을 정의
- 원칙의 모듈성 + 데이터와 메타데이터의 구분을 통해 특별한 상황의 문제들을 해결한다.
  - 매우 민감하거나 개인적으로 식별 가능한 데이터
    - 발견을 용이하게 하기 위한 풍부한 메타데이터의 공개는 데이터 자체의 FAIR publication이 없는 경우에도 높은 수준의 'FAIRness'을 제공
  - 비 데이터 연구 객체의 게시
    - 투명성과 과학적 재현성을 모두 달성하려면 공식적인 출판이 필요
    - FAIR 원칙은 데이터와 거의 동일한 방식으로 식별, 설명, 발견 및 재사용해야 하는 이러한 비데이터 자산에 동일하게 적용

## The Principles precede implementation
- Principle은 특정 구현 선택이 디지털 연구 자료를 찾을 수 있는지, 액세스할 수 있는지, 상호 운용성 및 재사용 가능한지를 평가
  
## Examples of FAIRness, and the resulting value-added
- Dataverse
  - 공개 커뮤니티 저장소 또는 기관 연구 데이터 저장소를 지원하기 위해 전세계에 설치된 오픈 소스 데이터 저장소 소프트웨어
  - 데이터 세트가 게시될 때 DOI(Digital Object Identifier) 또는 기타 영구적인 identifier(Handles)를 공개('F')
  - 이것은 메타데이터, 데이터 파일, 데이터 세트 용어, 면제 또는 라이센스 및 버전 정보에 대한 액세스를 제공하는 랜딩 페이지로 해결되며, 이 모든 정보는 인덱싱되고 검색 가능('F', 'A', 'R')
  - 메타데이터, 데이터 파일 및 데이터 및 분석('R')을 이해하는 데 필요한 모든 보완 파일(예: 문서 또는 코드)이 포함
  - 메타데이터는 개인 정보 보호 문제('F', 'A')를 위해 데이터가 제한되거나 제거되더라도 항상 공개
  - 메타데이터는 'I' 및 'R' FAIR 원칙을 광범위하게 지원하는 세 가지 수준으로 제공
    - 1) DataCite 스키마 또는 Dublin Core Terms에 매핑되는 data citation 메타데이터
    - 2) 가능한 경우 Science 도메인 내에서 사용되는 메타데이터 표준에 매핑되는 도메인별 메타데이터
    - 3) 표 형식의 데이터 파일(column level 메타데이터 포함)에 대해 깊고 광범위한 메타데이터를 제공
  - 데이터가 제한될 때, 액세스를 허용하는 토큰을 사용하여 데이터를 검색하고, 메타데이터에 액세스하고, 데이터 파일을 다운로드할 수 있는 공용 머신 액세스 인터페이스를 제공

- FAIRDOM (http://fair-dom.org/about)
  - 개별 연구 자산, 데이터 등은 유일하고 지속적인 HTTP URL로 식별되며, 이를 DOI에 등록하여 게시할 수 있다('F')
  - 자산은 개인 및/또는 개인 컴퓨터에 적합한 다양한 형식(RDF, XML)('I')으로 웹을 통해 액세스할 수 있습니다.
  - 메타데이터는 상호 운용성을 활성화하기 위해 RDF로 저장되며 자산을 다운로드하여 재사용할 수 있습니다('R')

- ISA
  - 생명과학 데이터 세트의 표준 준수 수집, 큐레이션, 관리 및 재사용을 용이하게 하는 커뮤니티 기반 메타데이터 추적 프레임워크
  - Nature Scientific Data의 Data Descriptor 기사와 많은 Giga Science 데이터 문서에 대한 구조화된 메타데이터를 제공하며, 다른 데이터 리소스 중에서 EBI MetaboLights 데이터베이스를 뒷받침

- Open PHACTS
  - 약물 발견과 관련된 정보를 위한 데이터 통합 플랫폼
  - 플랫폼에 대한 액세스는 인간(HTML)과 machine이 판독 가능한(RDF, JSON, XML, CSV 등) 다중 표현을 제공하는 machine 액세스 인터페이스를 통해 조정되며, 이는 FAIRness의 'A' 측면을 제공
  - ChEMBL URL을 제공하여 켐스파이더 또는 DrugBank와 같은 소스 정보를 검색
  - 데이터 세트의 대다수는 커뮤니티 합의 온톨로지('I')를 사용하여 설명

- wwPDB
  - 실험적으로 결정된 단백질과 핵산의 3D 구조에 대한 정보를 호스팅하는 특수 목적의 집중 큐레이션된 데이터 아카이브
  - wwPDB 메타데이터는 PubMed 및 NCBI Taxonomy와 같은 공통 식별자에 대한 상호 참조를 포함하고 있으며, 이들의 wwPDB 메타데이터는 화학 및 구조 생물학 영역에 대한 IUCr 데이터 표준('R')을 준수하는 데이터 사전 및 스키마 문서(http://mmcif.wwpdb.org 및 http://pdbml.wwpdb.org)에 설명되어 있다.
  - URL('F')을 통해 wwPDB 레코드에 대한 액세스를 제공하며, 모든 데이터와 메타데이터는 하나 이상의 wwPDB 관련 웹 사이트('F')를 통해 검색할 수 있다.

- UniProt
  - UniProt는 단백질 순서 및 주석 데이터를 위한 포괄적인 리소스
  - 150개 이상의 서로 다른 데이터베이스와 연동하여 모든 UniProt 레코드는 PubMed와 같은 광범위한 링크를 가지고 있어 풍부한 인용을 가능

- 메타데이터 게시 및 검색 가능성, 엄격한 개인 정보 보호 고려 사항의 경우 호환성, 데이터와 메타데이터 상호 운용성에 초점을 두어야 함!
  
## FAIRness is a prerequisite for proper data management and data stewardship
- 우수한 데이터 관리와 관리 기능은 그 자체가 목표가 아니라 지식 발견과 혁신을 지원하는 전제 조건
- 현대의 e-Science는 장기적으로 데이터를 찾을 수 있고, 액세스할 수 있으며, 상호 운용이 가능하며, 재사용할 수 있어야 함
- 모든 데이터 생산자와 출판사가 이러한 원칙을 검토하고 이행할 것을 요청하고, Force11 실무 그룹에 가입함으로써 FAIR 이니셔티브에 적극적으로 참여할 것을 촉구한다. 

