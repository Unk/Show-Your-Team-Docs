# Show Your Team API Documentation

1. 회원 User
    - [[POST] /api/users - 회원 가입](#post-api/users)
    - [[GET] /api/users/login - 로그인](#get-api/users/login)
    - [[GET] /api/users/logout - 로그아웃](#get-api/users/logout)
    - [[GET] /api/users - 내 정보 조회](#get-api/users)
    - [[POST] /api/users/size - 내 사이즈 입력](#post-api/users/size)
    - [[GET] /api/users/size - 내 사이즈 조회](#get-api/users/size)
2. 팀 Team

## <a name="post-api/users"></a>[POST] /api/users - 회원가입

### 헤더 Headers

불필요

### 요청 Request

| 필드명 | 데이터 타입 | 필수 | 조건 |
|------|------|------|------|
| user_id | string | required | 4자 이상, 10자 이하 |
| user_name | string | required |  |
| email | string | required | 이메일 형식 |
| password | string | required | 12자 이상, 16자 이하 |

### 응답 Response

`200 가입 성공`

    {
        "user_id": "user001",
        "user_name": "User",
        "email": "user@user.com"
    }

`400 잘못된 요청`, `409 충돌(Conflict)`

    {
        "error": "user_name은 필수 입력 항목입니다."
    }

## <a name="get-api/users/login"></a>[GET] /api/users/login - 로그인

### 헤더 Headers

불필요

### 요청 Request

| 필드명 | 데이터 타입 | 필수 | 조건 |
|------|------|------|------|
| user_id | string | required |  |
| password | string | required |  |

### 응답 Response

`200 로그인 성공`

    {
        "user_id": "user001",
        "user_name": "User",
        "email": "user@user.com",
        ...
        "token": "qwer-1234-asdf-5678"
    }

`400 잘못된 요청`

    {
        "error": "user_id는 필수 입력 항목입니다."
    }

## <a name="get-api/users/logout"></a>[GET] /api/users/logout - 로그아웃

### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 로그아웃 성공`

    {
        "result": true
    }

`400 잘못된 요청`, `401 인증 필요`

    {
        "error": "Not authenticated."
    }

## <a name="get-api/users"></a>[GET] /api/users - 내 정보 조회


### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    {
        "user_id": "user001",
        "user_name": "User",
        "email": "user@user.com",
        ...
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

## <a name="post-api/users/size"></a>[POST] /api/users/size - 내 사이즈 입력

### 설명 Description

사용자 신체 사이즈 입력. 수정 API를 겸한다.

### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

| 필드명 | 데이터 타입 | 필수 | 조건 |
|------|------|------|------|
| shoulder | float |  | 기본값 0 |
| chest | float |  | 기본값 0 |
| waist | float |  | 기본값 0 |
| pelvis | float |  | 기본값 0 |
| hip | float |  | 기본값 0 |
| thigh | float |  | 기본값 0 |
| arm_length | float |  | 기본값 0 |
| leg_length | float |  | 기본값 0 |

### 응답 Response

`200 입력 성공`

    {
        "shoulder": 0,
        "chest": 0,
        "waist": 0,
        "pelvis": 0,
        "hip": 0,
        "thigh": 0,
        "arm_length": 0,
        "leg_length": 0
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

## <a name="get-api/users/size"></a>[GET] /api/users/size - 내 사이즈 조회

### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    {
        "shoulder": 0,
        "chest": 0,
        "waist": 0,
        "pelvis": 0,
        "hip": 0,
        "thigh": 0,
        "arm_length": 0,
        "leg_length": 0
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }
