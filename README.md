# COME2US

## 프로젝트 개요

COME2US는 쿠팡·스마트스토어와 같은 실제 이커머스 서비스를 모델로 한
엔터프라이즈 **이커머스 플랫폼** 실습 프로젝트입니다.

본 리포지토리는 전체 프로젝트 중 **1차(MVP 구축 단계)** 에 해당하며,
빠른 기능 구현과 함께 향후 MSA 전환을 고려한 구조적 설계에 집중했습니다.

## 프로젝트 목표

* 일일 약 5,000명 트래픽을 처리 가능한 이커머스 MVP 구현

* 핵심 도메인(회원·상품·주문·결제) 기능 완성

* AWS 기반 재현 가능한 인프라 + 자동 배포 환경 구축

### 핵심 도메인 설계

1. 회원 / 인증

    * Spring Security + JWT 기반 인증·인가

    * Role 기반 권한 관리 (CUSTOMER, OWNER, MANAGER, MASTER)

2. 상점 / 상품

    * OWNER 1명당 1개 상점 구조

    * 옵션·이미지·카테고리(3단계) 관리

    * 상품 공개 / 숨김 처리

3. 주문 / 결제 / 환불

    * Toss Payments 결제 연동

4. 쿠폰 / 할인

    * 쿠폰 중복 적용 방지, 쿠폰 사용 이력 관리

5. 리뷰
  
    * 구매자만 리뷰 작성 가능

    * 리뷰 작성 시 상품 평점·리뷰 수 동기적 갱신

## ERD 
<img width="2500" height="1662" alt="MVP Architecture" src="https://github.com/user-attachments/assets/e3160d65-935f-415b-88aa-151c914550a9" />

## 인프라 및 배포 구성
<img width="1003" height="846" alt="infra" src="https://github.com/user-attachments/assets/f2a45864-53c9-4090-9d3a-5f5739a11c01" />

## 컴퓨트 & 런타임

* EC2 t3.medium

* Docker Compose

* Spring Boot Application

* Redis (JWT / 세션 관리)

## CI/CD

* Terraform 기반 IaC

* GitHub Actions

* Gradle Build

* Docker Image Build & Push

* EC2에서 Docker Image Pull 후 컨테이너 재시작

* .env 기반 런타임 환경 변수 관리

## 성능 테스트

<img width="1678" height="676" alt="image" src="https://github.com/user-attachments/assets/d974c23a-04f4-408f-bc68-422b3955c801" />


* JMeter 기반 부하 테스트

* 블랙프라이데이 트래픽 상황 가정

* 결과 : 평균 180 TPS, 평균 응답 시간 36ms

* 주문 트래픽 급증 시 일시적 장애 발생
