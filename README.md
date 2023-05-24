# 2023 1학기 Bigdata Analysis Lecture Data Analysis Project

## Project 절차

### 자료 가공 과정
 1. 선거 데이터 정리
    - 선거관리위원회 선거 데이터는 도-특별시 / 시군구 / 구 - 동읍면 / 선거 장소 순
    - 이중 시군구 단위를 기준으로 데이터를 정리하기 위해 동읍면의 ‘합계’를 기준으로 데이터 정리        
    - 검증과정을 통해 누락된 데이터를 채우는 과정을 거침.
    - 분석에 필요한 핵심 데이터 추출 : 야당 득표율 (2022년 기준 야당) 및 시군구별 투표율
 2. 통계청 및 교통 빅데이터 등 다양한 시군구 단위 지역 데이터 병합
    - 시군구 단위(구가 존재하는 시의 경우, ‘시 단위’, 특별시는 구 단위)로 데이터 병합 
    - 교통 데이터 전처리
    - Pivot 함수 활용하여 데이터 정리  
    - 비율로 바꾸는 것이 필요한 데이터 비율로 정리
    - 정리 후 병합
    - **병합 후 결측값 및 inf 확인**
    - 활용 및 사전 검토 자료
활용 변수	비고	Source
노인천명당 노인여가복지시설수		보건복지부 노인 복지시설 현황
녹지율		통계청 지역통계 / 한국토지주택공사
독거노인가구비율		통계청 인구총조사
빈집비율		통계청 주택총조사
걷기실천율		통계청 지역통계 / 질병관리청 지역사회건강조사
비만유병률		통계청 지역통계 / 질병관리청 지역사회건강조사
보건기관이용률		통계청 지역통계 / 질병관리청 지역사회건강조사
인플루엔자_예방접종률		통계청 지역통계 / 질병관리청 지역사회건강조사
우울감_경험률		통계청 지역통계 / 질병관리청 지역사회건강조사
흡연율		통계청 지역통계 / 보건복지부
의료인력현황		건강보험통계
유아천명당 보육시설수		한국도시통계
주민 1인당 생활계폐기물배출량		통계청 지역통계 / 행정안전부 환경부
화재발생건수		통계청 지역통계 / 소방청 화재현황통계
사회복지예산비중		통계청 지역통계 / 행정안전부 지방재정연감
천명당의료기관병상수		통계청 지역통계 / 건강보험심사평가원 지역의료이용통계 
50세 이상 인구비율		인구총조사 / 성 연령 및 세대구성별 인구
A.농업,임업및어업_인구비율		인구총조사 / 현거주지별 근무지별 산업별 취업인구
C.제조업_인구비율		인구총조사 / 현거주지별 근무지별 산업별 취업인구
노후주택비율		통계청 주택총조사
사업체수		전국사업체조사
실업률		통계청 지역별 고용조사
인구십만명당_문화기반시설수		통계청 지역통계 / 문화체육관광부 문화기반시설총람
청년고용률_2022.1/2		통계청 지역별고용조사
1인당_자동차등록대수		통계청 지역통계 / 국토교통부 자동차등록현황보고
도로포장률		통계청 지역통계 / 국토교통부
농업어업임업_부가가치 비율	농어입업 부가가치/총부가가치	각 시도별 경제활동별 지역내총생산
제조업_부가가치 비율	제조업 부가가치/총부가가치	각 시도별 경제활동별 지역내총생산
고등학교_도보대중교통_30분_이내_인구비율		국가교통 데이터베이스
병·의원_도보대중교통_30분_이내_인구비율		국가교통 데이터베이스
중학교_도보대중교통_30분_이내_인구비율		국가교통 데이터베이스
철도역_도보대중교통_30분_이내_인구비율		국가교통 데이터베이스
초등학교_도보대중교통_30분_이내_인구비율		국가교통 데이터베이스
재정자립도		통계청 지역통계 / 행정안전부
순이동_2021	순이동/전체인구	통계청 국내인구이동통계
대졸자합	대학교 4년제 이상	인구총조사 / 성, 연령, 혼인상태 및 교육정보별 인구
통근통학1시간미만	통근통학 시간 15분 이하 ~ 1시간 미만 합 / 전체인구	통계청 인구총조사 / 소요시간별 이용 교통수단별 통근 통학 인구
첨단산업_인구비율	금융보험업 종사자 + 첨단과학기술서비스업 종사자	인구총조사 / 현거주지별 근무지별 산업별 취업인구
공공기관_인구비율	국제기관 종사자 + 공무원	인구총조사 / 현거주지별 근무지별 산업별 취업인구
생활서비스업_부가가치	숙박음식점업 + 교육서비스업 + 보건사회복지서비스업 + 문화및기타서비스업	각 시도별 경제활동별 지역내총생산
특허3개년평균	2019~2021년 3개년 평균	기초지자체별 등록 특허건수
50세 이상 인구비율		인구총조사

- 기초 통계량과 상관분석
    1. 자료 분포
    2. 상관분석
    3. 기초통계량
- **적합도 검정**
    - ***KMO 측도*** : 
        - 각 변수 간 유의미한 상관관계가 있는지 확인
        
    - ***Bartlett 검정*** 
        - ‘구형성 검정’ : 자료가 일정한 관계 없이 퍼져 있는지 검정 ⇒ 변수 간 관계가 있는지 확인
        
### PCA
1. Factor Analysis → Communalities 0.5를 기준으로 변수를 걸러내는 작업
2. 변수를 걸러낸 이후 KMO 및 Bartlett 검정 진행
3. 선택된 변수로 Varimax, Equamax, Quartimax과 Principal Factor 기법을 사용해 Factor Analysis 진행
    - 상관행렬을 활용
    - Varimax의 결과가 비교적 깔끔하게 도출 : 다른 요인 회전 방식에 비해 상관성이 떨어지는 다양한 측면의 요인을 잘 도출해 우리의 분석 목적에 부합
    - Factor1-2 도출
        ![image](https://github.com/popper6508/202301bigdataanalysis/assets/118153199/c1eca5f7-f3f4-45cd-b57c-3781d44fdaac)

       
        
4. 도출된 Factor 기반으로 회귀분석 진행

- **기본적인 특성**
    - Factor1 특성
        ![image](https://github.com/popper6508/202301bigdataanalysis/assets/118153199/33555991-a113-47c8-b714-9a2a69230e22)


        - 수도권 및 광역시권과 나머지의 격차가 드러나는 지표 : 주로 인프라 혹은 생활 환경 여건 관련 지표로 볼 수 있다.
            - 수도권과 광역시권 주변은 어디든 상관없이 전반적으로 양호한 흐름
    - Factor2 특성
        ![image](https://github.com/popper6508/202301bigdataanalysis/assets/118153199/3e646eb7-86ee-43f6-9e1a-371498db5562)

  
        
        - 경기 남부 IT, 반도체 클러스터, 구미-창원-울산 중심의 제조업 클러스터 중심으로 양호한 흐름. 수도권 등 지역 내부에서도 다른 양상. 인프라와 생활 여건 관계없이 지역 내 부가가치 창출 수준에 따라 지표가 달라지는 흐름
            - 지역의 부가가치 창출 능력, 산업, 지역 내 인적자본 수준을 나타내는 지표로 해석 가능
    
    - factor1는 가까운 지역을 그대로 따라가기에 분포가 전반적으로 고르지만, factor는 지역군 내에서도 특정한 지역에 쏠리는 경향을 보이기에 대부분은 일정 수준 근방에 있지만 극단적으로 양호한 값을 보이는 지역 존재
    
    factor1는 가까운 지역을 그대로 따라가기에 분포가 전반적으로 고르지만, factor는 지역군 내에서도 특정한 지역에 쏠리는 경향을 보이기에 대부분은 일정 수준 근방에 있지만 극단적으로 양호한 값을 보이는 지역 존재
    
    - 전반적인 생활 인프라 여건과 경제 수준 중 무엇이 사람들의 투표 여부 의사결정에 큰 영향을 주는지 확인 가능.

- 주성분회귀
    - 확인한 포인트
        - 이분산 : 존재하는 것으로 확인 (이분산의 분포를 이용한 활용방안 있을 것)
        - 자기상관 (없는 것으로 확인)
        - 적합도 : R^2 (높은 적합성)
        - F-test : 결합 유의성 (통계적으로 유의)
        - 독립변수 각각의 유의성 : t-test (통계적으로 유의)

- 어떻게 활용할 수 있을까
 1. 비정치적 지표를 활용한 정치학 연구
 2. 지역별 선거 관리 자원 배치
 3. 마지막 유세 지역 등 선거전략 세팅
