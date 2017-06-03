# Show Your Team API Documentation

1. 회원 User
    - [[POST] /api/users - 회원 가입](#post-api/users)
    - [[POST] /api/users/login - 로그인](#post-api/users/login)
    - [[GET] /api/users/logout - 로그아웃](#get-api/users/logout)
    - [[GET] /api/users - 내 정보 조회](#get-api/users)
    - [[POST] /api/users/size - 내 사이즈 입력](#post-api/users/size)
    - [[GET] /api/users/size - 내 사이즈 조회](#get-api/users/size)
2. 팀 Team
    - [[POST] /api/teams - 팀 생성](#post-api/teams)
    - [[GET] /api/teams - 팀 정보 조회](#get-api/teams)
    - [[GET] /api/teams/search - 팀 검색](#get-api/teams/search)
    - [[GET] /api/teams/:id](#get-api/teams/:id)
    - [[PUT] /api/teams/:id](#put-api/teams/:id)
    - [[PUT] /api/teams/:id/signup](#put-api/teams/:id/signup)
    - [[GET] /api/teams/:id/signup](#get-api/teams/:id/signup)
    - [[GET] /api/teams/:id/member/accept](#get-api/teams/:id/member/accept)
    - [[DELETE] /api/teams/:id/member/reject](#delete-api/teams/:id/member/reject)
    - [[DELETE] /api/teams/:id/member/remove](#delete-api/teams/:id/member/remove)
    - [[POST] /api/teams/:id/member/add](#post-api/teams/:id/member/add)
    - [[PUT] /api/teams/:id/member/update](#post-api/teams/:id/member/update)
3. 리소스 Resource
    - [[GET] /api/resource - 패턴 목록](#get-api/resource)
    - [[GET] /api/resource/all - 리소스가 포함된 패턴 목록](#get-api/resource/all)
    - [[GET] /api/resource/:code - 패턴 코드로 리소스 정보 조회](#get-api/resource/:code)
4. 매거진 Magazine
    - [[GET] /api/magazine - 매거진 목록](#get-api/magazine)
    - [[GET] /api/magazine/:id - 매거진 상세](#get-api/magazine/:id)
5. 주문 Order
    - [[POST] /api/order - 커스텀 주문](#post-api/order)
6. 업로드 Upload
    - [[POST] /api/upload - 파일 업로드](#post-api/upload)

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

## <a name="post-api/users/login"></a>[POST] /api/users/login - 로그인

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

| 필드명 | 데이터 타입 | 필수 | 조건 |
|------|------|------|------|
| team_name | string | required |  |
| team_logo_url | string| required | URL 형식 |
| member_list | array | required |  |
| member_list[][ member_name ] | string | required |  |
| member_list[][ number ] | integer | required |  |
| member_list[][ user_id ] | integer |  | 고도 회원일 경우 회원 unique key (m_no) |

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

`400 잘못된 요청`, `401 인증 필요`

    {
        "error": "Not authenticated."
    }

## <a name="post-api/teams"></a>[POST] /api/teams - 팀 생성

### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |
| Content-Type | application/json |

### 요청 Request

{
  "teamName": "FC Toeo",
  "teamLogoUrl": "fileserver/folder/path",
  "memberList": [
    {
      "memberName": "teamUser11",
      "number": 52
    },
    {
      "memberName": "teamUser21",
      "number": 71
    }
  ]
}

### 응답 Response

`200 조회 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "teamId": 15,
      "memberList": [
        {
          "id": 22,
          "member_name": "teamUser11",
          "number": null
        },
        {
          "id": 23,
          "member_name": "teamUser21",
          "number": null
        }
      ],
      "waitingMemberList": []
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`400 잘못된 요청`
    {
        "erro": {field-name} 필드는 필수 입력 사항입니다.
    }

## <a name="get-api/teams"></a> [GET] /api/teams
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |
| Content-Type | application/json |

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

[
  {
    "team_name": "FC Toeo",
    "team_logo_url": "fileserver/folder/path",
    "team_id": 10,
    "member_list": [
      {
        "id": 12,
        "member_name": "teamUser11",
        "number": null
      },
      {
        "id": 13,
        "member_name": "teamUser21",
        "number": null
      }
    ],
    "waiting_member_list": [],
    "creation_date": "2017/06/03"
  },

  ...
]

`401 인증 필요`

    {
        "error": "Not authenticated."
    }


## <a name="get-api/teams/search"></a> [GET] /api/teams/search
## <a name="get-api/teams/:id"></a> [GET] /api/teams/:id
## <a name="put-api/teams/:id"></a> [PUT] /api/teams/:id

## <a name="get-api/resource"></a> [GET] /api/resource - 패턴 목록]

### 헤더 Headers

불필요

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    [
      {
        "id": 1,
        "code": "11000",
        "created_at": "2017-05-20 08:00:26",
        "updated_at": "2017-05-20 08:00:26"
      },
      ...
    ]

## <a name="get-api/resource/all"></a> [GET] /api/resource/all - 리소스가 포함된 패턴 목록]

### ! 주의 사항

이 API는 시범적으로 만들어졌습니다.
서버 부하에 유의하며 사용하시기 바랍니다.

### 헤더 Headers

불필요

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    [
        {
            "id": 1,
            "code": "11000",
            "created_at": "2017-05-20 08:00:26",
            "updated_at": "2017-05-20 08:00:26",
            "resources": [
                {
                    "id": 1,
                    "pattern_id": 1,
                    "code": "1",
                    "front": null,
                    "back": null,
                    "pants_left": null,
                    "pants_right": null,
                    "thumbnail": null,
                    "created_at": "2017-05-20 08:00:36",
                    "updated_at": "2017-05-23 06:56:14"
                },
                ...
            ]
        },
        ...
    ]

## <a name="get-api/resource/:code"></a> [GET] /api/resource/:code - 패턴 코드로 리소스 정보 조회]

### 헤더 Headers

불필요

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    [
        {
            "id": 1,
            "pattern_id": 1,
            "code": "1",
            "front": null,
            "back": null,
            "pants_left": null,
            "pants_right": null,
            "thumbnail": null,
            "created_at": "2017-05-20 08:00:36",
            "updated_at": "2017-05-23 06:56:14"
        },
        ...
    ]

`404 찾을 수 없음`

    {
        "error": "해당 코드의 패턴을 찾을 수 없습니다."
    }

## <a name="post-api/upload"></a> [POST] /api/upload - 파일 업로드

### 헤더 Headers

불필요

### 요청 Request

| 필드명 | 데이터 타입 | 필수 | 조건 |
|------|------|------|------|
| type | string | required | file, base64 중에 선택 |
| files | `multipart data` or `base64 string` | required |  |

`200 조회 성공`

    {
        "id": 1,
        "name": "72/8f/3cfe66735370c87414abc88dc35b.jpg",
        "hash": "728f3cfe66735370c87414abc88dc35b",
        "path": "storage/72/8f/3cfe66735370c87414abc88dc35b.jpg",
        "mime": "image/jpeg",
        "created_at": "2017-05-23 09:28:36",
        "updated_at": "2017-05-23 09:28:36"
    }

`400 잘못된 요청`

    {
        "error": "알 수 없는 type 입니다."
    }