# aicoder.com 内部哈工大接口文档

> 内部文档禁止分享

## 综述

只有登录相关的接口不需要添加认证的token,其余所有的接口请求都必须在请求头中添加 `Authorization`.

所有的请求对应模型都默认提供了: 添加、修改、查询、复杂查询和删除操作的api。

### 接口统一地址模型

接口地址符合`RestFul`风格。

+ 添加

| 标题  | 说明               | 备注                                        |
|-----|------------------|-------------------------------------------|
| 地址  | `POST /api/模型名字` | `header`中必须添加 `Authrization`对应的jwt的token. |

例如:

```js
$.ajax({
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:3002/api/user",
  "method": "POST",
  "headers": {
    "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MzcxODU3OTk5NzgsIm5hbWUiOiJzZGZmZmYifQ.WLVdU-GESQR6kJfUdLCBpNWUZMGAW6VsTk6lfAXC1xM"
  },
  "data": {
    "Name": "laomsds",
    "Passwd": "aaafc44445555",
    "isDel": "false"
  }
}).done(function (response) {
  console.log(response);
});
```

+ 修改

| 标题  | 说明                  | 备注                                        |
|-----|---------------------|-------------------------------------------|
| 地址  | `PUT /api/模型名字/:id` | `header`中必须添加 `Authrization`对应的jwt的token. |
支持`PATCH协议`

```js
$.ajax({
  "async": true,
  "crossDomain": true,
  "url": "http://%E4%BF%AE%E6%94%B9",
  "method": "PUT",
  "headers": {
    "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MzcxODU3OTk5NzgsIm5hbWUiOiJzZGZmZmYifQ.WLVdU-GESQR6kJfUdLCBpNWUZMGAW6VsTk6lfAXC1xM",
    "Content-Type": "application/x-www-form-urlencoded"
  },
  "data": {
    "Name": "laoma2333"
  }
}).done(function (response) {
  console.log(response);
});
```

+ 删除

| 标题  | 说明                     | 备注                                        |
|-----|------------------------|-------------------------------------------|
| 地址  | `DELETE /api/模型名字/:id` | `header`中必须添加 `Authrization`对应的jwt的token. |

```js
$.ajax({
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:3002/api/user/5b9621e7cad9bf1c60e1d51f",
  "method": "DELETE",
  "headers": {
    "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MzcxODU3OTk5NzgsIm5hbWUiOiJzZGZmZmYifQ.WLVdU-GESQR6kJfUdLCBpNWUZMGAW6VsTk6lfAXC1xM"
  }
}).done(function (response) {
  console.log(response);
});
```

+ 查询id

| 标题  | 说明                  | 备注                                        |
|-----|---------------------|-------------------------------------------|
| 地址  | `GET /api/模型名字/:id` | `header`中必须添加 `Authrization`对应的jwt的token. |

```js
$.ajax({
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:3002/api/user/5b9621e7cad9bf1c60e1d51f",
  "method": "GET",
  "headers": {
    "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MzcxODU3OTk5NzgsIm5hbWUiOiJzZGZmZmYifQ.WLVdU-GESQR6kJfUdLCBpNWUZMGAW6VsTk6lfAXC1xM"
  }
}).done(function (response) {
  console.log(response);
});
```

### 复合查询

| 标题     | 说明                                                                                             |
|--------|------------------------------------------------------------------------------------------------|
| 地址     | `GET /api/模型名字`                                                                                |
| 注意事项   | `header`中必须添加 `Authrization`对应的jwt的token.                                                      |
| 分页     | 当前页请求参数中,添加 `page`, 默认不分页.一页大小,请在请求参数中添加`limit`或`pageSize`. 例如:   `page=9&limit=10`,一页10条,第9页. |
| 排序     | 升序: `sort_asc=排序字段名`, 降序:`sort_desc=排序字段名`                                                     |
| 等于过滤   | `字段名_eq=等于的值`, 查询某个字段必须等于什么...                                                                 |
| 模糊查询过滤 | `字段名_like=模糊查询的值`                                                                              |

```js
$.ajax({
  "async": true,
  "crossDomain": true,
  "url": "http://localhost:3002/api/user?sort_asc=Passwd&limit=5&page=1",
  "method": "GET",
  "headers": {
    "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MzcxODU3OTk5NzgsIm5hbWUiOiJzZGZmZmYifQ.WLVdU-GESQR6kJfUdLCBpNWUZMGAW6VsTk6lfAXC1xM"
  }
}).done(function (response) {
  console.log(response);
});
```

## 登陆相关

### 登陆获取token

用户登录WebApp时，首先对用户进行鉴权。

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/userlogin` |
| 请求方式 | `POST`                                               |
| 数据类型 | `application/json`                                   |
| 特殊要求 | 后台限制同一指纹浏览器,在1分钟内只能请求5次,超过次数认为是攻击,则禁止登录.             |

#### 请求参数

| 序号  | 字段     | 类型     | 性质  | 说明   |
|-----|--------|--------|-----|------|
| 1   | username    | String | 必填  | 公司编号 |
| 2   | password | String | 必填  | 密 码   |

#### 返回值

| 序号  | 字段    | 类型     | 说明                |
|-----|-------|--------|-------------------|
| 1   | user  | Object | 登陆成功的用户对象信息       |
| 2   | code  | Number | 登陆成功的编码，1成功， 0失败。 |
| 3   | token | String | token密钥。          |
| 4   | msg   | String | 消息内容。             |

> 登录成功后续请求都需要添加token密钥到header的Authorization中。

用户对象类型

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| del         | Boolean  | false                    | 是否删除   |
| id           | Number | 1 | 主键     |
| username          | String   | vyk                      | 用户名    |
| passwd        | String   | 123123                   | 密码     |
| avatar        | String   | /a/b.png                 | 头像     |
| name         | String   | 郑霞                       | 中文名    |
| phone         | String   | 1555511215151            | 电话     |
| mail | Date     | lsf@mm.com               | 邮箱 |
| school    | String | 北京大学 | 学校   |
| isTeacher    | Boolean | true | 是否是老师   |

#### 返回实例

```js
// 登录成功消息
{
    "user": {
      id: 1000,
      username: 'wyd',
      password: 'aicoder.com',
      del: false,
      active: true, //  激活
      avatar: '/img/a1.png',
      name: "张三",
      school: '清华大学',
      mail: Random.email(),
      phone: '189222222',
      isTeacher: true
    },
    "code": 1,
    "msg": "登录成功",
    "token": "eyJ0eXAiOiJKV1..."
}

// 登录失败消息
{
  code: 0,
  msg: '用户名或者密码错误'
}
```

当前可以用的用户名密码：

用户名|密码|是否是老师
---|---|---
ngr|aicoder|否
wyd|aicoder|是
admin|aicoder|是
admin1|aicoder|是
