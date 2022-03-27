<p align="center">
    <img width="200px;" src="https://raw.githubusercontent.com/woowacourse/atdd-subway-admin-frontend/master/images/main_logo.png"/>
</p>
<p align="center">
  <img alt="npm" src="https://img.shields.io/badge/npm-%3E%3D%205.5.0-blue">
  <img alt="node" src="https://img.shields.io/badge/node-%3E%3D%209.3.0-blue">
  <a href="https://edu.nextstep.camp/c/R89PYi5H" alt="nextstep atdd">
    <img alt="Website" src="https://img.shields.io/website?url=https%3A%2F%2Fedu.nextstep.camp%2Fc%2FR89PYi5H">
  </a>
  <img alt="GitHub" src="https://img.shields.io/github/license/next-step/atdd-subway-service">
</p>

<br>

# 인프라공방 샘플 서비스 - 지하철 노선도

<br>

## 🚀 Getting Started

### Install
#### npm 설치
```
cd frontend
npm install
```
> `frontend` 디렉토리에서 수행해야 합니다.

### Usage
#### webpack server 구동
```
npm run dev
```
#### application 구동
```
./gradlew clean build
```
<br>


### 1단계 - 성능 테스트
1. 웹 성능예산은 어느정도가 적당하다고 생각하시나요
<br>네이버 : https://m.map.naver.com/subway/subwayLine.naver?region=1000
![네이버](./images/naver_metric.png)
![네이버](./images/naver_optimaztion.png)
![네이버](./images/naver_page_test.png)

----------
나의 서비스 : https://infra-study.p-e.kr/
![my](./images/my_metric.png)
![my](./images/my_optimization.png)
![my](./images/my_page_test.png)


사용자 체감상 1초 이내, 경쟁사 대비 20프로 이내의 성능
* fcp : 0.8초
* tti: 1초 이내
* speedIndex: 2초
* Largest Contentful Paint : 2초


2. 웹 성능예산을 바탕으로 현재 지하철 노선도 서비스는 어떤 부분을 개선하면 좋을까요 
* js파일 압축 사용 : gzip압축 
* 사용하지 않는 리소스 제거 
* keep-alive 사용
* 캐시설정

3. 부하테스트 전제조건은 어느정도로 설정하셨나요
* DAU : 100만  (추측)
* 처리량 : DAU(100만) * 2  = 200만
* 평균 rps = 200만 / 86,500  = 23
* 최대 rps = 평균 * 10 = 230
* Latency = 100ms(최대)

  
4. Smoke, Load, Stress 테스트 스크립트와 결과를 공유해주세요
<br> path를 변경해가면 3개의 시나리오를 테스트했습니다.

-------
접속 빈도가 높은 페이지 : https://infra-study.p-e.kr/

* vuser
  * R = 1
  * 231(최대rps) * 0.1(Latency) / 1(R) = 23
* 스크립트:
  * [smoke](./step1/main/smoke.js) : 시나리오 검증 테스트
  * [load](./step1/main/load.js) : 최대 rps 230을 기준으로 테스트
  * [stress](./step1/main/stress.js) : 최대 rps 2배이상을 기준으로 테스트

![smoke](./step1/main/1_smoke_test.png)
![load](./step1/main/1_load_test.png)
![stress](./step1/main/1_stress_test.png)

-------
데이터를 갱신하는 페이지 : https://infra-study.p-e.kr/lines

* vuser
  * R = 2
  * 231(최대rps) * 0.1(Latency) / 2(R) = 12
* 스크립트:
  * [smoke](./step1/lines/smoke.js) : 시나리오 검증 테스트
  * [load](./step1/lines/load.js) : 최대 rps 230을 기준으로 테스트
  * [stress](./step1/lines/stress.js) : 최대 rps 2배이상을 기준으로 테스트
![smoke](./step1/lines/smoke_test.png)
![load](./step1/lines/load_test.png)
![stress](./step1/lines/stress_test.png)

-------
데이터를 조회하는데 여러 데이터를 참조하는 페이지 : https://infra-study.p-e.kr/path

* vuser
  * R = 3
  * 231(최대rps) * 0.1(Latency) / 3(R) = 8
* 스크립트:
  * [smoke](./step1/path/smoke.js) : 시나리오 검증 테스트
  * [load](./step1/path/load.js) : 최대 rps 230을 기준으로 테스트
  * [stress](./step1/path/stress.js) : 최대 rps 2배이상을 기준으로 테스트

![smoke](./step1/path/smoke_test.png)
![load](./step1/path/load_test.png)
![stress](./step1/path/stress_test.png)
---

### 2단계 - 화면 응답 개선하기
1. 성능 개선 결과를 공유해주세요 (Smoke, Load, Stress 테스트 결과)

2. 어떤 부분을 개선해보셨나요? 과정을 설명해주세요

---

### [추가] 로깅, 모니터링
1. 각 서버내 로깅 경로를 알려주세요

2. Cloudwatch 대시보드 URL을 알려주세요
