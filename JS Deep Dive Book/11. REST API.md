# 1. REST API

- REST의 기본 원칙을 성실히 지킨 서비스 디자인을 ```RESTful```이라고 표현
- REST는 HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처이고, REST API는 REST를 기반으로 서비스 API를 구현한 것을 의미

# 2. REST API 설계 원칙

| HTTP 요청 메서드 | 종류    |       목적         | 페이로드 |
| --------------  | -----    |       ----         |---------|
| GET       | index/retrieve | 모든/특정 리소스 취득|    X    |
| POST      |   create       |   리소스 생성       |    O    |
| PUT       |    replace     |   리소스의 전체 교체|    O     |
| PATCH     |    modify      | 리소스의 일부 수정   |    O    |
| DELETE    |    delete      | 모든/특정 리소스 삭제|    X    |
