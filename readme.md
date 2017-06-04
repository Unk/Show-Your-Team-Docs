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
    - [[GET] /api/teams/:id/leave](#get-api/teams/:id/leave)
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
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "member_list": [
        {
          "member_name": "teamUser11",
          "number": 52
        },
        {
          "member_name": "teamUser21",
          "number": 71
        }
      ]
    }

### 응답 Response

`200 생성 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "team_id": 15,
      "member_list": [
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
      "waiting_member_list": []
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`400 잘못된 요청`

    {
        "error": {field-name} 필드는 필수 입력 사항입니다.
    }

## <a name="get-api/teams"></a> [GET] /api/teams
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

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


## <a name="get-api/teams/search"></a> [GET] /api/teams/search?keyword=:query
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    [
      {
        "team_name": "FC Toeo",
        "team_logo_url": "fileserver/folder/path",
        "team_id": 1,
        "member_list": [],
        "waiting_member_list": [],
        "creation_date": "2017/06/03"
      },
      ...
    ]

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`400 잘못된 요청`

    {
        "error": "keyword 필드는 필수 입력 사항입니다."
    }


## <a name="get-api/teams/:id"></a> [GET] /api/teams/:id
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    {
      "team_name": "newTeamName",
      "team_logo_url": "newTeamLogoUrl",
      "team_id": 1,
      "member_list": [],
      "waiting_member_list": [],
      "creation_date": "2017/06/03",
      "members": []
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
        "error": "팀을 찾을 수 없습니다."
    }



## <a name="put-api/teams/:id"></a> [PUT] /api/teams/:id
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |
| Content-Type | application/json |  |

### 요청 Request

    {
      "team_name": "newTeamName",
      "team_logo_url": "newTeamLogoUrl"
    }

### 응답 Response

`200 갱신 성공`
    
    {
      "team_name": "newTeamName",
      "team_logo_url": "newTeamLogoUrl",
      "team_id": 1,
      "member_list": [],
      "waiting_member_list": [],
      "creation_date": "2017/06/03"
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
        "error": "팀을 찾을 수 없습니다."
    }

## <a name="put-api/teams/:id/signup"></a> [PUT] /api/teams/:id/signup - 팀 가입 요청]
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 가입 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "team_id": 2,
      "member_list": [],
      "waiting_member_list": [
        {
          "id": 25,
          "member_name": "유저일이삼사",
          "number": null,
          "cloth_size": null,
          "user_email": null
        }
      ],
      "creation_date": "2017/06/03"
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
        "error": "already requested team"
    }

    {
        "error": "unknown team"
    }

## <a name="get-api/teams/:id/leave"></a> [GET] /api/teams/:id/leave - 팀 탈퇴]
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 탈퇴 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "team_id": 2,
      "member_list": [],
      "waiting_member_list": [],
      "creation_date": "2017/06/03"
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

## <a name="get-api/teams/:id/member/accept"></a> [GET] /api/teams/:id/accept?member_id=:member_id - 팀 가입 요청 승인]
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 승인 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "team_id": 2,
      "member_list": [],
      "waiting_member_list": [],
      "creation_date": "2017/06/03"
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
      "error": "Unauthorized user"
    }

    {
      "error": "unknown member"
    }

    {
      "error": "unknown team"
    }

    {
      "error": "already be accepted"
    }

    {
      "error": "not waiting member"
    }



## <a name="delete-api/teams/:id/member/reject"></a> [DELETE] /api/teams/:id/reject?member_id=:member_id - 팀 가입 거절]
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 거절 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "team_id": 2,
      "member_list": [],
      "waiting_member_list": [],
      "creation_date": "2017/06/03"
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
      "error": "Unauthorized user"
    }

    {
      "error": "unknown member"
    }

    {
      "error": "unknown team"
    }

    {
      "error": "already be accepted"
    }

    {
      "error": "not waiting member"
    }

## <a name="delete-api/teams/:id/member/remove"></a> [DELETE] /api/teams/:id/remove?member_id=:member_id - 팀 멤버 삭제]
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |

### 요청 Request

불필요

### 응답 Response

`200 삭제 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "team_id": 2,
      "member_list": [],
      "waiting_member_list": [],
      "creation_date": "2017/06/03"
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
      "error": "Unauthorized user"
    }

    {
      "error": "unknown member"
    }

## <a name="post-api/teams/:id/member/add"></a> [POST] /api/teams/:id/member/add - 팀 멤버 추가]
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |
| Content-Type | application/json |  |

### 요청 Request

    {
      "member_name": "user000",
      "number": 32,
      "cloth_size": "S"
    }

### 응답 Response

`200 추가 성공`

    {
      "team_name": "FC Toeo",
      "team_logo_url": "fileserver/folder/path",
      "team_id": 2,
      "member_list": [],
      "waiting_member_list": [],
      "creation_date": "2017/06/03"
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
      "error": "Unauthorized user"
    }

    {
      "error": "unknown team"
    }

## <a name="put-api/teams/:id/member/update"></a> [PUT] /api/teams/:id/member/update - 팀 멤버 속성 변경]
### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |
| Content-Type | application/json |  |

### 요청 Request

    {
      "member_id": 1,
      "member_name": "teamUser1",
      "number": 32,
      "cloth_size": "S" or "M" or "L" or "XL" ...
     }

### 응답 Response

`200 갱신 성공`

    {
      "id": 1,
      "member_name": "teamUser1",
      "number": 32,
      "cloth_size": "S",
      "user_email": null
    }

`401 인증 필요`

    {
        "error": "Not authenticated."
    }

`404 잘못된 요청`

    {
      "error": "Unauthorized user"
    }

    {
      "error": "incorrect team or member"
    }


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


## <a name="post-api/order"></a> [POST] /api/order - 주문하기

### 헤더 Headers

| 헤더명 | 값 | 예시 |
|-----|-----|-----|
| Authorization | Bearer {token-here} | Bearer qwer-1234-asdf-5678 |
| Content-Type | application/json |  |

### 요청 Request

    {
      "customItems": [
        {
          "productPart": "top, bottom",
          "productCategory": "uniform, shorts",
          "productName": "sleeves_round, sleeves_vneck, half_pants",
          "patternCode": "15030, 15031",
          "patternColor": 1,
          "colors": [
            {
              "partName": "body_neck",
              "colorCode": "#FFFFFF"
            }
          ],
          "name": {
            "font": 1,
            "colorCode": "#335222",
            "material": "material1"
          },
          "frontNumber": {
            "font": 1,
            "colorCode": "#335222",
            "material": "material1"
          },
          "backNumber": {
            "font": 1,
            "colorCode": "#335222",
            "material": "material1"
          },
          "frontSmallPatch": 2,
          "frontLargePatch": 2,
          "backLargePatch": 2,
          "armMediumPatch": 2,
          "fabric": "soft"
        }
      ],
      "members": [
        {
          "memberName": "teamUser1",
          "number": 32,
          "clothSize": "S, M, L, XL...",
          "userId": 23,
          "userEmail": "ewerw@ew.sa"
        }
      ],
      "customSizes": [
        {
          "sizeName": "L, XL",
          "quantity": 3
        }
      ],
      "quantity": 3
    }

`200 주문 성공`

    [
        "http://show-your-team-api.dev/order/1496509400_0_order.json"
    ]

`400 잘못된 요청`

    {
        "error": "failed save"
    }

## <a name="get-api/magazine"></a> [GET] /api/magazine - 매거진 목록

### 헤더 Headers

불필요

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    {
        "total": 1,
        "per_page": 12,
        "current_page": 1,
        "last_page": 1,
        "next_page_url": null,
        "prev_page_url": null,
        "from": 1,
        "to": 1,
        "data": [
            {
                "id": 2,
                "headline": "제목",
                "sub_headline": "부제",
                "main_image": "http://domain.com/storage/72/8f/3cfe66735370c87414abc88dc35b.jpg",
                "featured_image": "http://domain.com/storage/81/12/9b57ae6674d4482e054e0a3732fd.jpg",
                "created_at": "2017-05-23 09:42:31",
                "updated_at": "2017-06-04 16:20:37"
            }
        ]
    }

## <a name="get-api/magazine/:id"></a> [GET] /api/magazine/:id - 매거진 상세

### 헤더 Headers

불필요

### 요청 Request

불필요

### 응답 Response

`200 조회 성공`

    {
        "id": 2,
        "headline": "제목",
        "sub_headline": "부제",
        "main_image": "http://domain.com/storage/72/8f/3cfe66735370c87414abc88dc35b.jpg",
        "featured_image": "http://domain.com/storage/81/12/9b57ae6674d4482e054e0a3732fd.jpg",
        "content": "내용\r\n줄바꿈",
        "view_count": 1,
        "created_at": "2017-05-23 09:42:31",
        "updated_at": "2017-06-04 16:20:37"
    }

## <a name="post-api/upload"></a> [POST] /api/upload - 파일 업로드

### 헤더 Headers

불필요

### 요청 Request

| 필드명 | 데이터 타입 | 필수 | 조건 |
|------|------|------|------|
| type | string | required | file, base64 중에 선택 |
| file | `multipart data` or `base64 string` | required |  |

`200 업로드 성공`

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


    ### ! 주의 사항

이 API는 시범적으로 만들어졌습니다.
서버 부하에 유의하며 사용하시기 바랍니다.