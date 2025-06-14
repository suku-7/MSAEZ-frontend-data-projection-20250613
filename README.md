# Model
## MSAEZ-frontend-data-projection-20250613
MVVM 패턴 기반의 Vue.js 프론트엔드와 마이크로서비스 백엔드를 연동하여 클라우드 네이티브 애플리케이션을 구축한 것입니다.  
데이터 불일치를 방지하며 프론트엔드 중심의 데이터 프로젝션 방식을 구현하고 테스트했습니다.  

![스크린샷 2025-06-13 140223](https://github.com/user-attachments/assets/7f41ca79-2d2c-4a26-9e89-fc7bc4a2cd9f)
![스크린샷 2025-06-13 141144](https://github.com/user-attachments/assets/f6da7be7-dc2f-492a-a44b-442b24c4ce91)
![스크린샷 2025-06-13 141451](https://github.com/user-attachments/assets/fb02ea18-35e6-417a-aaf6-46fe5127bda0)
![스크린샷 2025-06-13 141507](https://github.com/user-attachments/assets/ffe6d3a0-5162-48b1-85f6-94acad0f80cc)
![스크린샷 2025-06-13 144811](https://github.com/user-attachments/assets/40811972-64d1-49f3-bdd2-0e5c7643d845)
![스크린샷 2025-06-13 150426](https://github.com/user-attachments/assets/7d6b92ef-aa18-4897-a709-3b820bca60be)
![스크린샷 2025-06-13 150455](https://github.com/user-attachments/assets/88034516-36cb-4cca-b6d5-626f03940b83)

---
## 터미널 작성 참고용
1. Java SDK 설치
프로젝트 구동에 필요한 Java Development Kit (JDK)를 설치합니다.  
```
sdk install java
```
2. Kafka 실행
메시지 브로커 역할을 하는 Kafka와 Zookeeper를 Docker Compose를 이용해 실행합니다.  
```
cd kafka/
docker-compose up -d
```
3. Order 및 Inventory 서비스 실행
백엔드의 Order (8081 포트) 및 Inventory (8082 포트) 마이크로서비스를 실행합니다.  
```
cd order
mvn clean spring-boot:run

# 새 터미널/세션에서 실행
cd inventory
mvn clean spring-boot:run
```
4. 프론트엔드 서비스 실행
Vue.js 기반의 프론트엔드 서비스 (8080 포트)를 실행합니다. npm i로 의존성을 설치한 후 npm run serve로 개발 서버를 구동합니다.  
```
cd frontend
npm i
npm run serve
```
5. Gateway 서비스 실행
각 마이크로서비스로의 요청을 라우팅하는 Gateway 서비스를 실행합니다.  
```
cd gateway
mvn spring-boot:run
```
6. 재고량 등록 및 웹사이트 확인  
HTTPie를 사용하여 Inventory 서비스에 재고량을 등록한 후, 웹사이트를 통해 주문 페이지에서 등록된 재고 정보를 확인합니다.  
```
pip install httpie
http :8082/inventories id=1 stock=10
```
웹사이트에서 확인:  
https://8088-msaschool-labshopcompen-n1oyzm85uys.ws-us120.gitpod.io/#/orders  

7. v-model 코드 수정
프론트엔드 코드 내 v-model을 활용하여 UI와 데이터 간의 양방향 바인딩을 조정하고 기본값을 설정하는 등의 수정을 진행합니다.  
