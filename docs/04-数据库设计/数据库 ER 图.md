# 表关系图

## 数据库表关系概览

### 核心实体关系

```
用户(User) 1:N 小说收藏(Collection)
用户(User) 1:N 播放记录(PlayHistory)
用户(User) 1:1 会员信息(VipInfo)
用户(User) 1:N 订单(Order)
小说(Novel) 1:N 章节(Chapter)
小说(Novel) 1:N 小说收藏(Collection)
章节(Chapter) 1:1 音频(Audio)
章节(Chapter) 1:N 播放记录(PlayHistory)
会员套餐(VipPackage) 1:N 订单(Order)
订单(Order) 1:N 支付记录(Payment)
```

## 详细实体关系说明

### 用户与相关实体

1. **用户 - 小说收藏**
   - 一个用户可以收藏多本小说
   - 一本小说可以被多个用户收藏
   - 关系类型：多对多（通过中间表 Collection 实现）

2. **用户 - 播放记录**
   - 一个用户可以有多条播放记录
   - 一条播放记录只属于一个用户
   - 关系类型：一对多

3. **用户 - 会员信息**
   - 一个用户最多有一条会员信息
   - 一条会员信息只属于一个用户
   - 关系类型：一对一

4. **用户 - 订单**
   - 一个用户可以创建多个订单
   - 一个订单只属于一个用户
   - 关系类型：一对多

### 内容与相关实体

5. **小说 - 章节**
   - 一本小说包含多个章节
   - 一个章节只属于一本小说
   - 关系类型：一对多

6. **小说 - 小说分类**
   - 一本小说可以属于多个分类
   - 一个分类可以包含多本小说
   - 关系类型：多对多（通过中间表 NovelCategory 实现）

7. **章节 - 音频**
   - 一个章节对应一个音频文件
   - 一个音频文件只对应一个章节
   - 关系类型：一对一

### 订单与支付

8. **订单 - 会员套餐**
   - 一个订单对应一个会员套餐
   - 一个会员套餐可以被多个订单购买
   - 关系类型：多对一

9. **订单 - 支付记录**
   - 一个订单可以有多个支付尝试记录
   - 一个支付记录只属于一个订单
   - 关系类型：一对多

## 外键关联表

| 表名 | 外键字段 | 引用表 | 引用字段 | 说明 |
|------|----------|--------|----------|------|
| Collection | userId | User | id | 用户ID |
| Collection | novelId | Novel | id | 小说ID |
| Chapter | novelId | Novel | id | 小说ID |
| Audio | chapterId | Chapter | id | 章节ID |
| PlayHistory | userId | User | id | 用户ID |
| PlayHistory | chapterId | Chapter | id | 章节ID |
| VipInfo | userId | User | id | 用户ID |
| Order | userId | User | id | 用户ID |
| Order | packageId | VipPackage | id | 会员套餐ID |
| Payment | orderId | Order | id | 订单ID |
| NovelCategory | novelId | Novel | id | 小说ID |
| NovelCategory | categoryId | Category | id | 分类ID |

## 数据流向说明

1. **用户注册/登录流程**
   - 用户信息存入 User 表
   - 生成 Token 返回给前端

2. **内容管理流程**
   - 小说信息存入 Novel 表
   - 章节信息存入 Chapter 表
   - 音频信息存入 Audio 表
   - 建立 Novel 和 Category 的关联关系

3. **用户行为流程**
   - 用户收藏小说：在 Collection 表中创建记录
   - 用户播放章节：在 PlayHistory 表中记录播放进度

4. **会员购买流程**
   - 用户选择套餐：查询 VipPackage 表
   - 创建订单：在 Order 表中插入记录
   - 支付处理：在 Payment 表中记录支付状态
   - 开通会员：更新 VipInfo 表中的会员信息