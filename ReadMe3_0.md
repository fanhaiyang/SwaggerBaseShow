### swagger 3.0.2版本
github地址：https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md#requestBodyObject
官网文档地址：https://swagger.io/specification/#parameterObject
```js

openapi: "3.0.0"
info:
  version: "1.0.0"
  title: My Swagger3.0接口
  description: Swagger3.0接口示例API
servers:
  - url: http://xxx.xxx/api

paths:
  /getUser:
    get:
      tags:
        - UserManage
      summary:''
      operationId: GetUser
      parameters:
        - name: userId
          in: query
          description: ''
          required: false
          schema:
            type: string
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GetData'
  /getUserCollection:
    get:
      tags:
        - UserManage
      summary: ''
      operationId: GetUserCollection
      parameters:
        - name: userIdLike
          in: query
          description: '模糊匹配，格式：userId.%'
          required: false
          schema:
            type: string
        - name: offset
          in: query
          description: '分页偏移量'
          required: false
          schema:
            type: integer
            format: int32
        - name: limit
          in: query
          description: '显示数量'
          required: false
          schema:
            type: integer
            format: int32
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GetDataList'
  /getAccount:
    get:
      tags:
        - UserManage
      summary: ''
      operationId: GetAccount
      parameters:
        - name: accountType
          in: query
          description: '账户产品类型'
          required: false
          schema:
            type: string
        - name: key
          in: query
          description: '用户userId'
          required: false
          schema:  
            type: string
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GetAccountData'
  /getAccountByList:
    get:
      tags:
        - UserManage
      summary: ''
      operationId: GetAccountList
      parameters:
        - name: accountType
          in: query
          description: 账号类型
          required: false
          schema:
            type: string
            
        - name: userIds
          in: query
          description: 用户Id集合
          required: false
          schema:
            type: array
            items:
              type: string
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GetBatchGroupAccountData'

  /addSubUser:
    post:
      tags:
        - UserManage
      summary: 添加子账户
      operationId: AddSubUser
      parameters:
        - name: userInfo
          in: query
          description: '用户信息'
          required: false
          schema:
            $ref: '#/components/schemas/UserInfos'
              
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GetData'              
  /updateUser:
    post:
      tags:
        - UserManage
      summary: ''
      operationId: UpdateUser
      parameters:
        - name: userInfo
          in: query
          description: ''
          required: false
          schema:
            $ref: '#/components/schemas/UserInfos'
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GetData'
  /updateLoginMode:
    post:
      tags:
        - UserManage
      summary: 更新账户登录状态
      operationId: UpdateLoginType
      parameters:
        - name: userId
          in: query
          description: '用户Id,批量账户以逗号隔开'
          required: false
          schema:
            type: string
        - name: mode
          in: query
          description: "0 ip自动登录\r\n1 用户名密码登录\r\n2 ip+用户名密码登录"
          required: false
          schema:
            type: integer
            format: int32
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GetData'
components:
  schemas:
    GetData:
      description: 获取用户信息
      type: object
      properties:
        message:
          description: ''
          type: string
        status:
          format: int32
          description: ''
          type: integer
        data:
          $ref: '#/components/schemas/UserInfos'
          description: ''
    
    UserInfos:
      type: object
      properties:
        userId:
          description: 用户ID
          type: string
        userRealname:
          description: 用户真实姓名
          type: string
        adminEmail:
          description: ''
          type: string
        userNickname:
          description: 昵称
          type: string
        password:
          description: 密码
          type: string
        isMale:
          format: int32
          description: "性别\r\n1--男、2--女"
          type: integer
        mobilePhone:
          description: 手机号
          type: string
        idcardNumber:
          description: 身份证号
          type: string
        educationLevel:
          format: int32
          description: "学历\r\n0--大专，1--本科，2--硕士，3--博士、4--其他"
          type: integer
        subject:
          description: 学科
          type: string
        dateBirth:
          format: date-time
          description: 出生日期
          type: string
        email:
          description: 邮箱
          type: string
        topical:
          description: 兴趣爱好
          type: string
        workUnit:
          description: 当前工作单位/院校
          type: string
        oldWorkUnit:
          description: 原工作单位/院校
          type: string
        title:
          format: int32
          description: "职称\r\n职称：0--初级、1--中级、2--副高级、3--正高级、4--其他；学者认证时填写的"
          type: integer
        isFreeze:
          format: int32
          description: "是否冻结\r\n1--冻结、2--解冻"
          type: integer
        avatarUrl:
          description: 用户头像
          type: string
        userRoles:
          format: int32
          description: "角色\r\n0--普通用户、1--认证用户、2--学者用户"
          type: integer
        isPhoneVerification:
          format: int32
          description: 是否手机验证通过
          type: integer
        isEmailVerification:
          format: int32
          description: Email是否验证通过
          type: integer
        registrationTime:
          format: date-time
          description: 注册时间
          type: string
        institution:
          description: 机构名
          type: string
        pid:
          description: 父ID
          type: string
        loginMode:
          format: int32
          description: "登录方式\r\n0--IP自动、1--用户名密码、2--IP+用户名密码"
          type: integer
        usertype:
          format: int32
          description: "用户类型\r\n1--机构管理员，2--机构账号，3--机构用户子账号，0--个人用户"
          type: integer
        extend:
          description: 扩展字段
          type: string
        userUsedname:
          description: 曾用名
          type: string
        graduatedSchool:
          description: 毕业院系
          type: string
          
    UserSearchRequest:
      description: 用户检索条件类
      type: object
      properties:
        userId:
          type: string
        userIdLike:
          type: string
        pId:
          type: string
        offset:
          format: int32
          type: integer
        limit:
          format: int32
          type: integer
    GetDataList:
      description: 获取用户信息列表信息
      type: object
      properties:
        message:
          description: ''
          type: string
        status:
          format: int32
          description: ''
          type: integer
        data:
          $ref: '#/components/schemas/UserInfoData'
          description: ''
    UserInfoData:
      type: object
      properties:
        items:
          uniqueItems: false
          type: array
          items:
            $ref: '#/components/schemas/UserInfos'
        totalCount:
          format: int32
          type: integer
        empty:
          type: boolean
          
    AccountId:
      type: object
      properties:
        accountType:
          type: string
        key:
          type: string
    GetAccountData:
      description: 获取机构账户财务信息
      type: object
      properties:
        message:
          description: ''
          type: string
        status:
          format: int32
          description: ''
          type: integer
        data:
          $ref: '#/components/schemas/BalanceLimitAccounts'
          description: ''
    BalanceLimitAccounts:
      type: object
      properties:
        payChannelId:
          description: 账户类型
          type: string
        beginDateTime:
          format: date-time
          description: 生效时间
          type: string
        endDateTime:
          format: date-time
          description: 失效时间
          type: string
        addDateTime:
          format: date-time
          description: 添加时间
          type: string
        id:
          format: int32
          type: integer
        userId:
          type: string
        balance:
          format: double
          type: number
        totalConsume:
          format: double
          type: number
    GetBatchGroupAccountData:
      description: 批量获取机构账户财务信息
      type: object
      properties:
        message:
          description: ''
          type: string
        status:
          format: int32
          description: ''
          type: integer
        data:
          $ref: '#/components/schemas/BatchGroupAccountData'
          description: ''
    BatchGroupAccountData:
      type: object
      properties:
        items:
          uniqueItems: false
          type: array
          items:
            $ref: '#/components/schemas/BalanceLimitAccounts'
        totalCount:
          format: int32
          type: integer
        empty:
          type: boolean
    GetAccountDataList:
      description: 获取用户购买产品列表信息
      type: object
      properties:
        message:
          description: ''
          type: string
        status:
          format: int32
          description: ''
          type: integer
        data:
          $ref: '#/components/schemas/AccountData'
          description: ''
    AccountData:
      type: object
      properties:
        items:
          description: ''
          uniqueItems: false
          type: array
          items:
            $ref: '#/components/schemas/BalanceLimitAccounts'
        totalCount:
          format: int32
          description: ''
          type: integer
        empty:
          description: ''
          type: boolean
tags:
  - name: MyTestApi
    description: ''

```
