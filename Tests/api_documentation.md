# 2046 R&B bar 小程序接口文档

本文档定义了2046 R&B bar小程序云开发所需的API接口。

## 基础信息

- 基础URL: `https://api.bar2046.com`
- API版本: v1
- 数据格式: JSON
- 授权方式: 请求头部包含 `Authorization: Bearer {token}`

## 通用响应格式

```json
{
  "code": 200,      // 状态码
  "message": "成功", // 状态消息
  "data": {}        // 返回数据
}
```

## 错误码说明

| 状态码 | 说明 |
|--------|------|
| 200    | 成功 |
| 400    | 请求参数错误 |
| 401    | 未授权 |
| 403    | 无权限 |
| 404    | 资源不存在 |
| 500    | 服务器内部错误 |

## 接口列表

### 1. 歌手相关接口

#### 1.1 获取推荐歌手列表

```
GET /api/v1/singers/recommended
```

**请求参数**:
- `limit`: 数量限制，默认5
- `skip`: 跳过记录数，用于分页，默认0

**响应示例**:
```json
{
  "code": 200,
  "message": "成功",
  "data": {
    "singers": [
      {
        "id": "singer123",
        "name": "Ella Johnson",
        "photoUrl": "https://example.com/photos/ella.jpg",
        "genre": "R&B / Soul",
        "nextPerformance": {
          "date": "2025-04-15T21:00:00Z",
          "venue": "2046 Live House"
        }
      },
      {
        "id": "singer456",
        "name": "Marcus Harper",
        "photoUrl": "https://example.com/photos/marcus.jpg",
        "genre": "Neo Soul / Jazz",
        "nextPerformance": {
          "date": "2025-04-18T20:30:00Z",
          "venue": "2046 Live House"
        }
      }
    ]
  }
}
```

#### 1.2 获取最新歌手列表

```
GET /api/v1/singers/latest
```

**请求参数**:
- `limit`: 数量限制，默认5
- `skip`: 跳过记录数，用于分页，默认0

**响应示例**:
```json
{
  "code": 200,
  "message": "成功",
  "data": {
    "singers": [
      {
        "id": "singer789",
        "name": "Sarah Chen",
        "photoUrl": "https://example.com/photos/sarah.jpg",
        "genre": "Contemporary R&B",
        "nextPerformance": {
          "date": "2025-04-22T21:30:00Z",
          "venue": "2046 Live House"
        }
      },
      {
        "id": "singer101",
        "name": "James Wilson",
        "photoUrl": "https://example.com/photos/james.jpg",
        "genre": "Soul / Funk",
        "nextPerformance": {
          "date": "2025-04-25T22:00:00Z",
          "venue": "2046 Live House"
        }
      }
    ]
  }
}
```

#### 1.3 获取歌手详情

```
GET /api/v1/singers/{singerId}
```

**响应示例**:
```json
{
  "code": 200,
  "message": "成功",
  "data": {
    "id": "singer123",
    "name": "Ella Johnson",
    "photoUrl": "https://example.com/photos/ella.jpg",
    "coverUrl": "https://example.com/covers/ella.jpg",
    "genre": "R&B / Soul",
    "biography": "Ella Johnson，知名R&B和Soul歌手，以其独特的声音和感染力强的现场表演而闻名...",
    "works": [
      {
        "id": "album1",
        "title": "Soul Reflection",
        "type": "专辑",
        "releaseYear": "2022",
        "trackCount": 10
      },
      {
        "id": "song1",
        "title": "Midnight Dreams",
        "type": "单曲",
        "releaseYear": "2023",
        "trackCount": null
      }
    ],
    "performances": [
      {
        "id": "perf1",
        "date": "2025-04-15T21:00:00Z",
        "venue": "2046 Live House",
        "eventName": "2046 R&B 之夜"
      },
      {
        "id": "perf2",
        "date": "2025-04-29T20:00:00Z",
        "venue": "2046 Live House",
        "eventName": "Jazz & Cocktail Night"
      }
    ]
  }
}
```

#### 1.4 收藏/取消收藏歌手

```
POST /api/v1/singers/{singerId}/favorite
```

**请求体**:
```json
{
  "favorite": true  // true表示收藏，false表示取消收藏
}
```

**响应示例**:
```json
{
  "code": 200,
  "message": "收藏成功",
  "data": {
    "isFavorited": true
  }
}
```

### 2. 活动相关接口

#### 2.1 获取活动列表

```
GET /api/v1/events
```

**请求参数**:
- `type`: 活动类型，可选值：upcoming（近期）, popular（热门）, favorite（收藏）
- `limit`: 数量限制，默认10
- `skip`: 跳过记录数，用于分页，默认0

**响应示例**:
```json
{
  "code": 200,
  "message": "成功",
  "data": {
    "events": [
      {
        "id": "event123",
        "title": "2046 R&B 之夜",
        "imageUrl": "https://example.com/events/rnb-night.jpg",
        "date": "2025-04-15T21:00:00Z",
        "location": "2046 Live House",
        "performers": ["Ella Johnson", "Marcus Harper"]
      },
      {
        "id": "event456",
        "title": "Soul Music Festival",
        "imageUrl": "https://example.com/events/soul-fest.jpg",
        "date": "2025-04-22T19:30:00Z",
        "location": "2046 Live House",
        "performers": ["Sarah Chen", "James Wilson"]
      }
    ]
  }
}
```

#### 2.2 获取活动详情

```
GET /api/v1/events/{eventId}
```

**响应示例**:
```json
{
  "code": 200,
  "message": "成功",
  "data": {
    "id": "event123",
    "title": "2046 R&B 之夜",
    "imageUrl": "https://example.com/events/rnb-night.jpg",
    "date": "2025-04-15T21:00:00Z",
    "endTime": "2025-04-15T23:00:00Z",
    "location": "2046 Live House",
    "address": "北京市朝阳区三里屯街道",
    "performers": [
      {
        "id": "singer123",
        "name": "Ella Johnson"
      },
      {
        "id": "singer456",
        "name": "Marcus Harper"
      }
    ],
    "description": "2046 R&B 之夜将带您进入一场沉浸式的音乐体验，我们邀请了知名R&B歌手Ella Johnson和Marcus Harper为您带来精彩的现场表演..."
  }
}
```

#### 2.3 收藏/取消收藏活动

```
POST /api/v1/events/{eventId}/favorite
```

**请求体**:
```json
{
  "favorite": true  // true表示收藏，false表示取消收藏
}
```

**响应示例**:
```json
{
  "code": 200,
  "message": "收藏成功",
  "data": {
    "isFavorited": true
  }
}
```

### 3. 用户相关接口

#### 3.1 微信登录

```
POST /api/v1/auth/login
```

**请求体**:
```json
{
  "code": "wx_login_code",  // 微信登录返回的code
  "userInfo": {             // 用户允许的情况下提供
    "nickName": "小红",
    "avatarUrl": "https://example.com/avatar.jpg",
    "gender": 2
  }
}
```

**响应示例**:
```json
{
  "code": 200,
  "message": "登录成功",
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "userId": "user123",
    "expireIn": 7200
  }
}
```

#### 3.2 获取用户收藏列表

```
GET /api/v1/users/me/favorites
```

**请求参数**:
- `type`: 收藏类型，可选值：singers（歌手）, events（活动）

**响应示例**:
```json
{
  "code": 200,
  "message": "成功",
  "data": {
    "singers": [
      {
        "id": "singer123",
        "name": "Ella Johnson",
        "photoUrl": "https://example.com/photos/ella.jpg",
        "genre": "R&B / Soul",
        "nextPerformance": {
          "date": "2025-04-15T21:00:00Z",
          "venue": "2046 Live House"
        }
      }
    ]
  }
}
```

#### 3.3 获取用户评论

```
GET /api/v1/users/me/comments
```

**请求参数**:
- `type`: 评论类型，可选值：singers（歌手）, events（活动）
- `limit`: 数量限制，默认10
- `skip`: 跳过记录数，用于分页，默认0

**响应示例**:
```json
{
  "code": 200,
  "message": "成功",
  "data": {
    "comments": [
      {
        "id": "comment123",
        "content": "非常棒的表演！",
        "createTime": "2025-04-10T14:30:00Z",
        "targetType": "singer",
        "targetId": "singer123",
        "targetName": "Ella Johnson"
      }
    ]
  }
}
```

#### 3.4 添加评论

```
POST /api/v1/comments
```

**请求体**:
```json
{
  "targetType": "singer",  // singer 或 event
  "targetId": "singer123",
  "content": "非常期待下次的演出！"
}
```

**响应示例**:
```json
{
  "code": 200,
  "message": "评论成功",
  "data": {
    "id": "comment456",
    "content": "非常期待下次的演出！",
    "createTime": "2025-04-15T15:20:00Z",
    "targetType": "singer",
    "targetId": "singer123"
  }
}
```

#### 3.5 用户设置更新

```
PUT /api/v1/users/me/settings
```

**请求体**:
```json
{
  "notification": {
    "newEvents": true,
    "favoriteSingerEvents": true,
    "comments": false
  }
}
```

**响应示例**:
```json
{
  "code": 200,
  "message": "设置更新成功",
  "data": {
    "settings": {
      "notification": {
        "newEvents": true,
        "favoriteSingerEvents": true,
        "comments": false
      }
    }
  }
}
```

## 云开发数据库设计

以下是微信小程序云开发数据库集合设计方案：

### 1. singers 集合
存储歌手信息

```javascript
{
  _id: "singer123",
  name: "Ella Johnson",
  photoUrl: "cloud://xxx.jpg",
  coverUrl: "cloud://xxx.jpg", 
  genre: "R&B / Soul",
  biography: "歌手简介...",
  works: [{
    title: "Soul Reflection",
    type: "专辑",
    releaseYear: "2022",
    trackCount: 10
  }],
  createTime: new Date(),
  updateTime: new Date()
}
```

### 2. events 集合
存储活动信息

```javascript
{
  _id: "event123",
  title: "2046 R&B 之夜",
  imageUrl: "cloud://xxx.jpg",
  startTime: new Date("2025-04-15T21:00:00Z"),
  endTime: new Date("2025-04-15T23:00:00Z"),
  location: "2046 Live House",
  address: "北京市朝阳区三里屯街道",
  performers: [{
    id: "singer123",
    name: "Ella Johnson"
  }],
  description: "活动描述...",
  status: "upcoming", // upcoming, ongoing, finished
  createTime: new Date(),
  updateTime: new Date()
}
```

### 3. users 集合
存储用户信息

```javascript
{
  _id: "user123",
  openid: "wx_openid",
  userInfo: {
    nickName: "小红",
    avatarUrl: "https://xxx.jpg",
    gender: 2
  },
  settings: {
    notification: {
      newEvents: true,
      favoriteSingerEvents: true,
      comments: false
    }
  },
  createTime: new Date(),
  updateTime: new Date()
}
```

### 4. favorites 集合
存储用户收藏信息

```javascript
{
  _id: "fav123",
  userId: "user123",
  targetType: "singer", // singer 或 event
  targetId: "singer123",
  createTime: new Date()
}
```

### 5. comments 集合
存储用户评论

```javascript
{
  _id: "comment123",
  userId: "user123",
  userName: "小红",
  userAvatar: "https://xxx.jpg",
  targetType: "singer", // singer 或 event
  targetId: "singer123",
  content: "非常棒的表演！",
  createTime: new Date()
}
```

### 6. performances 集合
存储演出安排

```javascript
{
  _id: "perf123",
  singerId: "singer123",
  singerName: "Ella Johnson",
  eventId: "event123",
  eventName: "2046 R&B 之夜",
  date: new Date("2025-04-15T21:00:00Z"),
  venue: "2046 Live House",
  createTime: new Date()
}