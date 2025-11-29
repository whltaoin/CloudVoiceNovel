# 接口清单（URL、请求参数、返回结果）

## 用户模块接口

### 1. 用户注册
- **URL**: `/api/auth/register`
- **方法**: `POST`
- **请求参数**:
  ```json
  {
    "username": "string", // 用户名
    "email": "string", // 邮箱
    "password": "string", // 密码
    "confirmPassword": "string" // 确认密码
  }
  ```
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "注册成功",
    "data": {
      "userId": "string",
      "username": "string",
      "email": "string",
      "token": "string"
    }
  }
  ```

### 2. 用户登录
- **URL**: `/api/auth/login`
- **方法**: `POST`
- **请求参数**:
  ```json
  {
    "email": "string", // 邮箱
    "password": "string" // 密码
  }
  ```
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "登录成功",
    "data": {
      "userId": "string",
      "username": "string",
      "email": "string",
      "token": "string",
      "isVip": boolean
    }
  }
  ```

### 3. 获取用户信息
- **URL**: `/api/user/profile`
- **方法**: `GET`
- **请求头**: `Authorization: Bearer {token}`
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "userId": "string",
      "username": "string",
      "email": "string",
      "avatar": "string",
      "isVip": boolean,
      "vipExpireDate": "string"
    }
  }
  ```

### 4. 更新用户信息
- **URL**: `/api/user/profile`
- **方法**: `PUT`
- **请求头**: `Authorization: Bearer {token}`
- **请求参数**:
  ```json
  {
    "username": "string", // 可选
    "avatar": "string" // 可选
  }
  ```
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "更新成功",
    "data": {
      "userId": "string",
      "username": "string",
      "email": "string",
      "avatar": "string"
    }
  }
  ```

## 小说模块接口

### 1. 获取小说列表
- **URL**: `/api/novels`
- **方法**: `GET`
- **请求参数**:
  - `page`: 页码
  - `pageSize`: 每页数量
  - `category`: 分类（可选）
  - `keyword`: 关键词搜索（可选）
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "list": [
        {
          "novelId": "string",
          "title": "string",
          "author": "string",
          "cover": "string",
          "category": "string",
          "description": "string",
          "chapterCount": number,
          "totalDuration": number,
          "isVip": boolean
        }
      ],
      "total": number,
      "page": number,
      "pageSize": number
    }
  }
  ```

### 2. 获取小说详情
- **URL**: `/api/novels/{novelId}`
- **方法**: `GET`
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "novelId": "string",
      "title": "string",
      "author": "string",
      "cover": "string",
      "category": "string",
      "description": "string",
      "chapterCount": number,
      "totalDuration": number,
      "isVip": boolean,
      "isCollected": boolean,
      "lastReadChapter": number,
      "lastReadProgress": number
    }
  }
  ```

### 3. 获取章节列表
- **URL**: `/api/novels/{novelId}/chapters`
- **方法**: `GET`
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "chapters": [
        {
          "chapterId": "string",
          "chapterNumber": number,
          "title": "string",
          "duration": number,
          "isVip": boolean,
          "progress": number
        }
      ]
    }
  }
  ```

### 4. 收藏/取消收藏小说
- **URL**: `/api/novels/{novelId}/collect`
- **方法**: `POST`
- **请求头**: `Authorization: Bearer {token}`
- **请求参数**:
  ```json
  {
    "isCollect": boolean
  }
  ```
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "操作成功",
    "data": {
      "isCollected": boolean
    }
  }
  ```

## 音频模块接口

### 1. 获取音频播放信息
- **URL**: `/api/chapters/{chapterId}/audio`
- **方法**: `GET`
- **请求头**: `Authorization: Bearer {token}`
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "audioUrl": "string",
      "duration": number,
      "progress": number,
      "novelId": "string",
      "chapterId": "string",
      "chapterTitle": "string",
      "nextChapterId": "string",
      "prevChapterId": "string"
    }
  }
  ```

### 2. 保存播放进度
- **URL**: `/api/chapters/{chapterId}/progress`
- **方法**: `POST`
- **请求头**: `Authorization: Bearer {token}`
- **请求参数**:
  ```json
  {
    "progress": number // 播放进度（秒）
  }
  ```
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "保存成功"
  }
  ```

### 3. 下载音频（离线）
- **URL**: `/api/chapters/{chapterId}/download`
- **方法**: `POST`
- **请求头**: `Authorization: Bearer {token}`
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "下载链接生成成功",
    "data": {
      "downloadUrl": "string",
      "expiresIn": number
    }
  }
  ```

## 会员模块接口

### 1. 获取会员信息
- **URL**: `/api/vip/info`
- **方法**: `GET`
- **请求头**: `Authorization: Bearer {token}`
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "isVip": boolean,
      "vipLevel": number,
      "expireDate": "string",
      "remainingDays": number
    }
  }
  ```

### 2. 获取会员套餐
- **URL**: `/api/vip/packages`
- **方法**: `GET`
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "packages": [
        {
          "packageId": "string",
          "name": "string",
          "duration": number, // 天数
          "price": number,
          "originalPrice": number,
          "description": "string"
        }
      ]
    }
  }
  ```

### 3. 创建会员订单
- **URL**: `/api/vip/order`
- **方法**: `POST`
- **请求头**: `Authorization: Bearer {token}`
- **请求参数**:
  ```json
  {
    "packageId": "string",
    "paymentMethod": "string"
  }
  ```
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "订单创建成功",
    "data": {
      "orderId": "string",
      "orderAmount": number,
      "paymentUrl": "string"
    }
  }
  ```

## 推荐模块接口

### 1. 获取推荐小说
- **URL**: `/api/recommend/novels`
- **方法**: `GET`
- **请求参数**:
  - `type`: 推荐类型（"hot", "new", "personalized"）
  - `limit`: 返回数量
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "获取成功",
    "data": {
      "novels": [
        {
          "novelId": "string",
          "title": "string",
          "cover": "string",
          "isVip": boolean
        }
      ]
    }
  }
  ```

### 2. 记录阅读行为
- **URL**: `/api/behavior/read`
- **方法**: `POST`
- **请求头**: `Authorization: Bearer {token}`
- **请求参数**:
  ```json
  {
    "novelId": "string",
    "chapterId": "string",
    "readTime": number, // 阅读时长（秒）
    "progress": number
  }
  ```
- **返回结果**:
  ```json
  {
    "code": 200,
    "message": "记录成功"
  }
  ```