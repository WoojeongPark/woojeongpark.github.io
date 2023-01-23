---

title:  "[Review] MIMIC-IV Release"
excerpt: "논문 리뷰"

categories: [Study, Standard, Review]
tags:
  - [미믹, 의료정보, 의료, 정보, MIMIC, DB, 데이터베이스]

toc: true
toc_sticky: true
 
date: 2023-01-23
last_modified_at: 2023-01-23
math: true
comments : true
mermaid: true

---

# Review : MIMIC-IV, a freely accessible electronic health record dataset
## date : 2023. 01. 17.
## presenter : Woojeong Park

---

## Abstract
- 보통 데이터는 연구랑 부관한 archival system에 저장됨
- 주된 목표가 연구, 분석과 해석보다는 효율적 저장에 치중되어 있음
- 그래서 Beth Israel Deaconess Medical Center(이하 BIDMC)의 EHR에서 MIMIC-IV 공개!
- 임상 연구 수행에 대한 장벽을 없애는데 기여할 것

---

## Background
- EHR 데이터는 쌓여만 가는데, 연구지원에는 한계가 많음(noisy ...)
- 특히 ICU(중환자)는 면밀히 모니터링해서 데이터가 아주 많음
- __MIMIC__ : waveform database with demographics (>=90 patients)
- __MIMIC-II__ : 다양한 디지털 정보 시스템으로부터 sample size 증대시킴
- __MIMIC-III__ : MIMIC-II 에서 더 확장하여 >40000 patients

---

- 다른 곳도 이런 데이터 제공하는 곳 많음
  - EiCU-CRD(EiCU Collaborative Research Database) v2.0 : 수백 개의 개별 병원에 걸쳐 있는 DB
  - AmsterdamUMCdb
  - HiRID database : high-resolution physiologic variable 포함
  - Pediatric Intensive Care(PIC) : 소아 환자 포
- 이들과 다른 MIMIC-IV의 차별점
  - 2008-2019년인 10년 기간 다룸. + contemporary
  - 중환자 데이터 많음   
  - EHR은 새로운 정밀 디지털 정보 소스를 내포하고 있음
  - Modular organization을 구성하여 DB를 외부 부서 및 고유한 데이터 양식에 연결할 수 있음
---


![](/assets/img/230123/20230116194602.png)  
- Acquistion
  - BIDMC(병원데이터) + metavision(ICU 정보시스템) + external
- Transformation
  - SQL로 various data source -> single schema
- Deidentification
  - selectively remove protected health info. from reformatted schema


---

## Methods
- MIMIC-IV : BIDMC와 MIT의 합작
- BIDMC가 주변 풍조와 다르게, 연구데이터 공유를 허가해줬다

### Acquisition
- MIMIC-IV에는 general clinical care, monitoring, provider orders, billing 포함
- MSSQL server DB에 병원 데이터 가져오고, VPN로 MIT PostgreSQL DB system으로 보냄
- code system definition같은 외부데이터들은 독립적으로 가져와서 MIT PostgreSQL DB에 로드

---

#### Clinical cohort
- BIDMC에서 2008-2019년 ICU 데이터 얻어옴
- 개인정보가 강화되어있거나 18세 미만인 환자는 제외
- 동일인물 데이터는 병합
- BIDMC의 EHR은 MetaVision이라고 불리는 데이터웨어하우스에 접근해 얻음.
- PGLoader 라는 툴을 통해 MIT로 전송
  
---

#### External data sources
- Diagnosis Related Groups (DRGs), the International Classification of Diseases(ICD), the Healthcare Common Procedure Coding System (HCPCS) 등
  - DRG는 All Payer (AP-DRG), Medicare Severity (MS-DRG) 2개의 coding system을 로드
  - ICD는 매년 업데이트되어서 우리의 10년치 코호트는 최신버전에서 많이 제거되었는데, 이를 되살려 쓸 수 있도록 ICD 차원 테이블을 각각의 2020 버전으로 패치함. 지금 존재하지 않는 코드들은 과거에 사용된 코드들을 반복해서 채움
  - 구체적으로 v9, v10에 대해 ICD 코드 얻어서 업데이트함. 코드는 CMS(centers for Medicare & Medicaid Services) 얻음
    - ICD-9-CM, ICD-9-PCS, ICD-10-CM, and ICD-10-PCS.


---

#### Out-of-hospital mortality
- BIDMC와 SSDMF(Social Security Death Master File)와 연결은 시도하지 않았다.(품질문제 때문)
- 대신, Massachusetts State Registry of Vital Records and Statistics에 연결함. 여기서 이름-주민번호-생년월일 연결해서 records와 매칭시키는 custom algorithm 만듬
  - (성과 이름 - 주민번호 - 성과 생일) 중 하나라도 일치하면 생성하도록 하는 매칭 알고리즘
  - fuzzy matching 방식을 통해 많이 일치하는 것을 상위권 순위에 두도록 랭킹화
  - Jaro-Winkler edit distance for 이름, Levenshtein edite distance for 주민번호 or date-specific edit distance for dates 순서대로 랭킹
- BIDMC EHR에 590,325명 -> 150,832명이 알고리즘 결과로 나왔고, 65,805명을 state death records와 연결함.
- 51022명 : 성-생년월일-주민등록번호 일치
- 11634명 : 성-생년월일 일치 혹은 이름 비슷한 것
  
---

### Transformation
- SQL 이용. MIMIC-III와 backward compatibility 유지하고자 함.
- MIMIC-IV는 relational structure를 선택함.
  - 3가지 모듈 존재 : hosp, icu, note
  - 모듈? 출저와 내용이 유사한 정보의 하위 집합
  - modular structure는 미래에 MIMIC-IV를 다른 곳에서 가져온 데이터와 쉽게 연동하기 위한 것
- __hosp__ : ADT(Admission입원, Discharge퇴원, Transfer이동) 데이터, 실험실값, 미생물 배양, 투약 지시, 병원 행정데이터 등(외래 진료소 데이터 포함)
- __icu__ : ICU 병상 데이터. 정맥 주입, 환자 출력, 차트 데이터
- __note__ : 퇴원 요약, 방사선 보고
- free text와 structured information의 페어링을 서포트하기 위해서 single entity-attribute-value 테이블을 만들었다. 예를 들어, radiology_detail 테이블은 방사선 보고서로 수집되는 quantative information을 포함하고 있다.
- 이들을 모두 만든 뒤, RFC-4180  memo에 따라 테이블들은 csv로 export하였다.

---

### Deidentification
- Health Insurance Portability and Accountability Act (HIPAA) Safe Harbor provision은 18개의 identifiers 내포한 set을 제공한다. 
  - deidentify 항목들을 제공한다는 말
- HIPAA idnetifier 찾기 위한 custom algorithm 제작했다.
- Lookup table 이용하여 unique identifier인 subject_id를 환자에게, hadm_id는 병원에게 무작위 할당하고, 평행이동 교란을 실시하여 time point 유지
- PHI == Protected Health Information. 이들을 제거하기 위한 알고리즘을 만들기 위해 알려진 2개의 알고리즘을 결합해서 사용했다.
- 하나는 PHI 식별 시, DB에서 제거하고 3개의 underbar "___"로 대체하는 것. 이를 free text와 note module의 clinical note에도 적용함
-  인적 검토도 수행하여 검토함.

---

## Data Records
- MIMIC-IV 데이터 액세스는 PhysioNet19를 통해 제공된다. 
- hosp, icu module : PhysioNet20 의 MIMIC-IV 프로젝트에서 사용가능
- note module : PhysioNet21 의 Deidentified free text 임상 메모 프로젝트에서 사용 가능
  
---

- ICU 환자 인구통계
  - ![center](/assets/img/230123/20230116205537.png)  
- 심정지로 중환자실에 입원하여 일반 병동으로 퇴원하고, 수술 후 중환자실에 재입원 후 집으로 퇴원하는 환자의 그림


---
![center](/assets/img/230123/20230116205648.png)  
  - vital sign : 맨 위에 표시. 초기에 temperature가 많이 측정되었는데, 이는 targeted temperature management를 위함. 다양한 source들은 가운데 표시됨. 
  - 맨 밑에는 laboratory measurements 표시. ICU에서만 vital sign을 자주 측정하지만, lab measurement는 입원기간 내내 사용가능하다.

---

### Hospital module(hosp)
- ADT 데이터, 병원 행정데이터, 약물 처방 및 투여 등 포함
- subject_id : 모든 테이블에 존재하며, 환자 테이블의 demographic에 연결 가능
- hadm_id : 모든 테이블에 존재하며, 단일 입원 나타냄
  - hadm_id 없는 행은 외부에서 integrate된 것
- emar, poe 같은 테이블들은 detail이라는 테이블과 연결된다.(emar_detail and peo_detail)


---

#### Patient tracking
- demographic과 병원 내 이동은 3개의 테이블인 patients, admissions, trasnfers에 나타남
- 환자들은 subject_id를 할당받았고, patients 테이블은 유니크한 subject_id를 행마다 가짐
- 정확한 환자 체류 날짜를 de-identify하기 위해 anchor_year 라는 컬럼도 포함되어 있다. 
  - anchor_age==50이고 anchor_year==2150이라면, 2150년에 50살이 된다는 뜻
  - anchor_year_group == 2011-2013이면 deidentified인 2150년에 발생하는 모든 hospitalization은 2011-2013에 발생했다고 보고, 이 기간에 50세였음을 말함.
  - `anchor_year_group이 MIMIC-IV에 추가됨` : 시간이 흐름에 따라서 의료행위릐 변화를 통합적으로 분석하는데 도움이 될 것!
- dod 열에서 date of death 확인 가능
  - 퇴원일로부터 1년을 기준으로 검열됨
  - 사망날짜 없다 == 그 시점까지는 살아있었다
  
---

#### Administration
- hosp module의 tree table은 service, poe, poe_detail같은 행정정보 제공한다.
- service 테이블 : 환자가 입원한 병원 관련 service 제공
- poe, poe_detail 테이블 : Provider order entry 제공
  - POE system은 병원에서 diagnosis, imaging, consultation, treatment 고나련된 order를 생성하는데 쓰이는 시스템
  - order의 date, time도 제공한다.(x-ray study, medication order, nutrition order 등). 

---

#### Billing
- billing info는 diagnoses_icd, procedures_icd, drgcodes, hcpcsevents 테이블에 존재
- diagnoses_icd 테이블 : 질병코드 
  - International Classification of Diseases, Ninth Revision, Clinical Modification (ICD-9-CM)
  - ICD Tenth Revision, Clinical Modification (ICD-10-CM)
- d_icd_diagnoses : definition for ICD codes 제공
- seq_num : 대략적인 진단순서 제공. 단일병원에 최대 39개의 진단이 청구될 수 있음
  
  
---

- diagnoses는 ICD-9-CM이나 ICD-10-CM 온톨로지로 기록되고, 절차는 ICD-9/10-PCS로 기록됨. 위에서 기술한대로 매년 업데이트되는 항목이기에 모든 시점에서 유효한 코딩을 실시함
- DRG(diagnosis related group) : 입원 비용 할당에 청구되는 코드
- drg_type : 열에 주어진 행에 대한 온톨로지 저장
- d_hcpcsevents : 최종 청구 테이블
- hcpcsevents : mechanical ventilation, provision of ICU care 등에서 제공되는 청구 정보 포함
  
---

#### Measurement
- 환자 표본에서 가져온 측정은 미생물 이벤트나 lab event에 사용가능(in d_labitems 테이블)
- labevents 테이블 > specimen_id 열, microbiologyevents 테이블 > micro_specimen_id 열은 여러번 측정되는데, 이 경우 동일한 specimen_id 공유함
- 미생물 측정량은 단일 테이블에 저장되었고, 최종 해석 결과들이 storetime column에 포함되어 있음
- omr 테이블 : 환자의 온라인 의료기록인 OMR을 포함함. BIDMC 산하기관 방문한 환자정보도 문서화했음
  - `MIMIC-IV부터 OMR에는 혈압, 키, 체중, 체질량 지수, eGFR(expected GFR) 포함`

---

#### Medication
- prescriptions, pharmacy, emar, emar_detail 테이블이 존재
- prescriptions : provider가 내린 주문내역 포함
- pharmacy : 약물에 대한 정보 포함
- emar, emar_detail : eMAR(전자 의약품 관리 기록)
  - emar_id : 행 고유식별
  - emar_seq : 연대순으로 단조증가하는 정수 할당
  - poe_id, pharmacy_id 사용하면 각각 poe 및 pharmacy 테이블에 연결 가능함
  - emar : emar_detail은 일대다 대응

---

- ![center](/assets/img/230123/20230116212941.png)  
  - 투약 정보 시각화 of hadm_id 28503629
  - 회색 선 : 환자가 머무는 동안의 치료 병동 이름
  - bolus는 marker, 연속 주입 시 선으로 표시하고 투약 범위는 박스표시
  - 5일차에 이 환자는 헤파린의 two active prescription을 받았는데, 하나는 갈색 상자의 1600-3500 용량 헤파린, 다른 것은 핑크삼각형의 1000 용량을 받았다. 추가적으로 emar(오렌지색 원)에 따른 헤파린 투여를 받았고, 즉시 심장 병동으로 이동함
  
---

### ICU module(icu)
- ICU 입원 환자들의 데이터소스
- chartevents, d_items, datetimeevents, icustays, inputevents, outputevents, procedureevents 
- itemid 정의 위해 d_item 참조하고, stay_id 정의하기 위해 icustays 참조
- stay_id : icustays 테이블의 primary key
- icustays : transfer 테이블 in hosp module 참조. intime, outtime 포함
- icu stay 각각에 대응되는 transfer는 stay_id에 할당된다.(transfer가 여러개여도)
- datetimeevents : 마지막 투석시간과 같은 날짜 관련 이벤트들이 저장됨
- inputevents : 볼루스 투여와 같은 데이터들이 starttime, endtime, rate와 함께 저장됨. amount도
- outputevents : value, charttime 포함
- procedureevents : starttime, endtime such as mechanical ventilation
- chartevents : event table 중 가장 큼. 각 행은 charttime이고, subject_id, hadm_id, stay_id, storetime을 모두 가짐

---

### Notes module(note)
- free text들 포함
- 퇴원, 영상의학 소견 관련 테이블 제
- discharge : patients' history
  - 주증상, 현 병력, 과거 병력, procedure of disease, 신체검사, 퇴원진단 등
  - de-identification 위해 사회 기록 및 퇴원 지침 섹션은 제거됨(사회적 정보 포함되어 있어서)
  - 보조정보는 _detail 사용하여 entity-attribute-value 테이블인 discharge_detail에 저장함.
- radiology : 영상의학 전문의 보고서가 포함됨
  - x-ray, CT, MRI 등 영상정보 포함
  - radiology_detail : 방사선과 검사를 위한 코드화된 온톨로지와 연구에 대한 CPT(Current Procedure Terminology)를 제공함. 보고서에 대한 부록이 있는 경우, 연결된 note_id 제공

---

### Building on earlier versions of MIMIC
- MIMIC-III와 동일한 이름을 갖는 테이블은 호환된다.
- 주요 변경사항
- ![center](/assets/img/230123/20230116215027.png)  
- 모든 identifer가 MIMIC-IV 과정에서 재생성되었다. 그래서 MIMIC-III과 데이터 숮비 기간이 겹치더라도(2008-2012), subject_id와 같은 identifier로 연결이 불가능하다. 
- MIMIC-III(2002-2008) 및 MIMIC-IV(2008-2019) 기간에 걸친 연구를 지우너하기 위해 MIMIC-III Clinical Database CareVue subset을 지원한다. 이는 MIMIC-IV에는 없는 MIMIC-III 만이 갖는 patients data를 제공한다.

---

## Technical Validation
- 과학자와 임상의가 MIMIC-IV를 개발과정에서 평가하고 코드리뷰하고 티켓시스템 사용하여 문제를 추적했다.
- Code : was managed using version control software
- Data transformation was executed with a single, reproducible build script
- Validation of the build process : assessed data integrity, data consistency, and deidentification
- Unit tests were created to apply these chekcs during development

---

- Integrity check 사용 for ensuring integrity of the db structure.
  - 예를 들어, diagnositcs_icd의 각 진단 코드가 관련된 dimension table인 d_icd_diagnoses에 있는지 확인
  - 환자데이터 포함하는 모든 테이블에 대해 연결된 항목이 있는지 확인하는 것. accept table 사용하여 hadm_id 열이 있는 테이블에 대해 test
- consistency test for 알려진 사실과 정보가 유사한가?
  - ICU 입원에는 모든 청구된 진단이 있어야 함. 즉, icustays 테이블에 있는 hadm_id의 99% 이상은 diagnositcs_icd 테이블에 있어야 함
  - icustays 테이블에 있는 icu stays의 99%가 chartevents 테이블에서 적어도 하나의 heart rate measurement를 가지고 있어야 함.
  - 이전 버전의 MIMIC과 비교하여 labevents 테이블의 itemid subset이 MIMIC-III와 일치함을 확인
- deidentification test : deidentification pipeline이 잘 되었나?
  - 테이블의 열에 대한 모든 unique value를 추출하고, 모든 값들이 manually curated allow list에 있는지 확인

---

## Usage Notes
- 임상 치료에 대한 많은 정보 포함함.

### Access
- MIMIC-IV에 접근하고 싶다면 반드시 공동연구자와 함께 training course를 완강하고 sign a data use aggrement(DUA) 서약한다.
- DUA : 데이터세트 보호하고, 재식별화 하지 않고, 공유하지 않고, 비식별화 관련 문제는 보고할 것을 약속
  
---

### Derived tables
- MIMIC Code Repository는 원래 MIMIC-III를 위해 만들어졌었는데, 연구자가 재사용가능하도록 하기 위함이었다. SQL 스크립트를 잘 쓰라고...
- MIMIC-IV에도 이러한 문화를 유지할 것이다. III에서 쓰던 것이 많이 넘어왔다.
- 가능한 경우, MIMIC-IV와 그 코드들을 통해서 재구성한 데이터를 클라우드에서 직접 사용해볼 수 있게 했다.
- 또한, 주피터나 Rmarkdown으로 예제 분석 및 자습서 공유했다
- 우리가 제공한 데이터를 완전히 재현하는 소스코드를 공개했으니, 잘 쓰길 바람
  
---

## Code availability
- 환자정보 때문에 전체를 다 공개할 수는 없다.
- deidentification approach는 rule based + neural network 활용했는데, 둘다 publicly available.
- https://mimic.mit.edu


---
## https://mimic.mit.edu/docs/
- MIMIC-IV contains data from 2008-2019. The data was collected from Metavision bedside monitors.
- MIMIC-III contains data from 2001-2012. The data was collected from Metavision and CareVue bedside monitors.
- MIMIC-II contains data from 2001-2008. The data was collected from CareVue bedside monitors. 
  - MIMIC-II is no longer publicly available but the data can still be obtained from MIMIC-III by only including data from the CareVue monitors.


---
## https://github.com/MIT-LCP/mimic-code/

- [Example](https://github.com/MIT-LCP/mimic-code/blob/main/mimic-iv/notebooks/tableone.ipynb)