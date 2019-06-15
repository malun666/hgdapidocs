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

## 验证码地址

地址：http://192.168.1.130:8888/api/code

后台返回 svg的内容。

前端使用：

```html
<embed src="http://192.168.1.130:8888/api/code" type="image/svg+xml" />
或者图片
<img src="http://192.168.1.130:8888/api/code" alt="Breaking Borders Logo" height="65" width="68">
```

## 文件上传

文件上传限制文件大小： 2M，目前只支持上传一张图片。

上传地址： `http://192.168.1.130:8888/api/upload`

请求参数：

```sh
请求表单中，文件对应的name必须为： imgF
```

上传图片后，返回内容：

```js
{ img: `图片地址` }
// 例如：
{ img: '/server/upload/a.png'}
```

> 后台图片存放在192.168.1.130服务器上。

## 登陆相关

### 登陆获取token

用户登录WebApp时，首先对用户进行鉴权。

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/userlogin` |
| 请求方式 | `POST`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
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
ngr|aicoder.com|否
wyd|aicoder.com|是
admin|aicoder.com|是
admin1|aicoder.com|是

## 用户操作接口

### 获取用户

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/user` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 后台限制同一指纹浏览器,在1分钟内只能请求5次,超过次数认为是攻击,则禁止登录.             |

#### 请求用户的参数

| 序号  | 字段     | 类型     | 性质  | 说明   |
|-----|--------|--------|-----|------|
| 1   | id    | String | 必填  | 用户的ID |

#### ——返回值

返回一个数组，数组里面的对象是查询的当前用户的信息。

| 序号  | 字段    | 类型     | 说明                |
|-----|-------|--------|-------------------|
| 1   | id  | Number | 用户ID       |
| 2   | del  | Boolean | 是否删除 |
| 3   | username | String | 用户名          |
| 4   | password   | String | 密码             |
| 5   | avatar   | String | 头像             |
| 6   | name   | String | 姓名             |
| 7   | mail   | String | 邮箱             |
| 8   | phone   | String | 电话             |
| 9   | isTeacher   | Boolean | 是否老师             |

例如：

```js
[
    {
        "id": 1000,
        "username": "wyd",
        "password": "aicoder.com",
        "del": false,
        "active": true,
        "avatar": "http://192.168.1.130:8888/server/img/a1.png",
        "name": "张三",
        "school": "清华大学",
        "mail": "y.ajomofyh@hdeju.tj",
        "phone": "189222222",
        "isTeacher": true
    }
]
```

### 添加用户

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/user` |
| 请求方式 | `POST`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 后台限制同一指纹浏览器,在1分钟内只能请求5次,超过次数认为是攻击,则禁止登录.             |

参考json-server的添加

### 修改用户

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/user/{id}` |
| 请求方式 | `PUT`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 后台限制同一指纹浏览器,在1分钟内只能请求5次,超过次数认为是攻击,则禁止登录.             |

参考json-server的添加

### 删除用户

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/user/{id}` |
| 请求方式 | `DELETE`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 后台限制同一指纹浏览器,在1分钟内只能请求5次,超过次数认为是攻击,则禁止登录.             |

参考json-server的添加

## 学生端接口

### 获取轮播图接口

学生端首页显示的轮播图列表

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/student/carousel` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 轮播图请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是轮播图的数据。

```js
[{轮播图数据}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| order           | Number | 1 | 排序     |
| title          | String   |     美丽景色                  | 轮播图标题    |
| imgUrl        | String   | /a/b.png                 | 图片地址     |
| url         | String   | /home/a.html                       | 跳转地址    |

#### 返回实例

```js
// 获取成功返回的内容
[
    {
        "order": 1,
        "title": "美丽景色",
        "imgUrl": "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1555293675&di=a807c0f74255accb5380165976293a84&imgtype=jpg&er=1&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01398c5942618ca8012193a3f97976.jpg",
        "url": "http://www.aicoder.com"
    },
    {
        "order": 2,
        "title": "美丽景色1",
        "imgUrl": "http://www.33lc.com/article/UploadPic/2012-10/2012101714102663437.jpg",
        "url": "/login.html"
    },
    {
        "order": 3,
        "title": "美丽景色2",
        "imgUrl": "http://www.33lc.com/article/UploadPic/2012-10/2012101714103954400.jpg",
        "url": "/"
    }
]

// 未登录，返回失败消息，状态码是401
{
  code: 8,
  msg: '用户没有登录，不能访问'
}
```

### 获取学生端推荐课程列表

学生端首页推荐教材列表

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/student/courses?_limit=8&_order=id&isHot=true` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是推荐课程的数据。

```js
[{推荐教材数据1},{推荐教材数据2}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| id           | Number | 1 | 主键，课程编号     |
| catId           | Number | 1 | 分类的id     |
| title          | String   |        史蒂夫23路径               | 课程标题    |
| img        | String   | /a/b.png                 | 课程图片地址 小图    |
| bgimg        | String   | /a/b.png                 | 课程图片地址 大图    |
| press         | String   | 清华出版社                     | 出版社    |
| subon         | String   |     2019-04-09 10:13:21                 | 发布日期    |
| author         | String   |    李思              | 作者    |
| college         | String   |    清华大学              | 大学    |
| author         | String   |    李思              | 作者    |
| price         | String   |    30              | 价格    |
| textbook         | String   |    说明              | 课程内容说明    |
| catalog         | String   |                  | 课程课时说明    |
| isHot         | Boolean   |    true          | 是否热    |
| isrecommend         | Boolean   |    true          | 是否推荐    |
| studycount         | Number   |    10          | 购买人数    |
| teacherId         | Number   |    10          | 所属教师    |
| invitecode         | String   |    10          | 邀请码    |
| studytime         | String   |    "2019-05-01 10:05:20"         | 开始学习时间    |

#### 返回实例

```js
[
  {
      "id": 1,
      "title": "间位特更战",
      "subon": "2019-04-09 10:13:21",
      "author": "邓艳",
      "college": "东南大学",
      "img": "http://dummyimage.com/183x160",
      "bgimg": "http://dummyimage.com/320x278",
      "press": "清华出版社",
      "price": 86,
      "textbook": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p>",
      "aboutauthor": "<p>韩少功，1953年出生于湖南长沙，祖籍湖南澧县 [1]  。著名作家。</p><p>曾获境内外奖项：1980年、1981年全国优秀短篇小说奖；2002年法国文化部颁发的“法兰西文艺骑士奖章”；2007年第五届华语文学传媒大奖之“杰出作家奖”；第四届鲁迅文学奖；美国第二届纽曼华语文学奖等。作品分别以十多种外国文字共三十多种在境外出版。另有译作《生命中不能承受之轻》（昆德拉著）、《惶然录》（佩索阿著）等数种出版</p>",
      "studycount": 137,
      "studytime": "2019.2.13-2019.12.30",
      "invitecode": "00293099",
      "catalog": "<p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p>",
      "isHot": true,
      "isrecommend": false,
      "catId": 16,
      "simimg": "http://dummyimage.com/185x160",
      "teacherId": 3
  },
  {
      "id": 2,
      "title": "属器权",
      "subon": "2019-04-09 10:13:21",
      "author": "石芳",
      "college": "东南大学",
      "img": "http://dummyimage.com/183x160",
      "bgimg": "http://dummyimage.com/320x278",
      "press": "清华出版社",
      "price": 96,
      "textbook": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p>",
      "aboutauthor": "<p>韩少功，1953年出生于湖南长沙，祖籍湖南澧县 [1]  。著名作家。</p><p>曾获境内外奖项：1980年、1981年全国优秀短篇小说奖；2002年法国文化部颁发的“法兰西文艺骑士奖章”；2007年第五届华语文学传媒大奖之“杰出作家奖”；第四届鲁迅文学奖；美国第二届纽曼华语文学奖等。作品分别以十多种外国文字共三十多种在境外出版。另有译作《生命中不能承受之轻》（昆德拉著）、《惶然录》（佩索阿著）等数种出版</p>",
      "studycount": 148,
      "studytime": "2019.2.13-2019.12.30",
      "invitecode": "00293099",
      "catalog": "<p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p>",
      "isHot": true,
      "isrecommend": false,
      "catId": 10,
      "simimg": "http://dummyimage.com/185x160",
      "teacherId": 3
  }
]
```

### 获取学生端推荐教材

学生端首页推荐教材列表

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/student/materials?_limit=8&_order=id&isHot=true` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是推荐课程的数据。

```js
[{推荐教材数据1},{推荐教材数据2}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| id           | Number | 1 | 主键，课程编号     |
| catId           | Number | 1 | 分类的id     |
| title          | String   |        史蒂夫23路径               | 教材标题    |
| imgUrl        | String   | /a/b.png                 | 教材图片地址     |
| press         | String   | 清华出版社                     | 出版社    |
| deadline         | String   |     2019-04-09 10:13:21                 | 截止权限日期    |
| author         | String   |    李思              | 作者    |
| college         | String   |    清华大学              | 大学    |
| author         | String   |    李思              | 作者    |
| price         | String   |    30              | 价格    |
| description         | String   |    说明              | 教材内容说明    |
| ISBN         | String   |    000000000              | ISBN号    |
| author_des         | String   |    xx              | 作者介绍    |
| cat_des         | String   |                  | 分类说明    |
| isHot         | Boolean   |    true          | 是否热    |
| count         | Number   |    10          | 购买人数    |
| relevant_material         | Object   |              | 关联教材    |
| courseware_set         | Object   |              | 教材集    |
| question_bank         | Object   |              | 题库    |

#### 返回实例

```js
// 获取成功返回的内容
[
 {
    "id": 17,
    "catId": 8,
    "title": "产小何劳心社报米长",
    "imgUrl": "http://dummyimage.com/300/00405d/FFF&text=aicoder.com",
    "author": "张艳",
    "price": 41,
    "deadline": "2004-01-15 13:29:19",
    "relevant_material": [
        {
            "id": 54,
            "title": "求后物",
            "ISBN": "830000000002"
        },
        {
            "id": 13,
            "title": "示式往可",
            "ISBN": "830000000002"
        }
    ],
    "courseware_set": {
        "id": 10,
        "name": "构任小后",
        "count": 35
    },
    "question_bank": {
        "exercises": 467,
        "examination_paper": 269,
        "name": "气重段运"
    },
    "ISBN": "1000003200230",
    "description": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问</p>",
    "author_des": "<p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p>",
    "cat_des": "<p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p>",
    "isHot": true,
    "count": 127
  },
  {
    "id": 18,
    "catId": 14,
    "title": "导团可机意广们深打位况",
    "imgUrl": "http://dummyimage.com/300/00405d/FFF&text=aicoder.com",
    "author": "杜超",
    "price": 86,
    "deadline": "2009-08-18 02:24:47",
    "relevant_material": [
        {
            "id": 73,
            "title": "林何军于性",
            "ISBN": "830000000002"
        },
        {
            "id": 34,
            "title": "样只军七",
            "ISBN": "830000000002"
        }
    ],
    "courseware_set": {
        "id": 7,
        "name": "除再什",
        "count": 29
    },
    "question_bank": {
        "exercises": 797,
        "examination_paper": 123,
        "name": "加厂单动你法温"
    },
    "ISBN": "1000003200230",
    "description": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问</p>",
    "author_des": "<p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p>",
    "cat_des": "<p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p>",
    "isHot": true,
    "count": 60
  }
]

// 未登录，返回失败消息，状态码是401
{
  code: 8,
  msg: '用户没有登录，不能访问'
}
```

### 获取学生端分类数据接口

课程分类数据：用于教材和课程。

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/student/course_category` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是推荐课程的数据。

```js
[{分类数据},{分类数据}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| id           | Number | 1 | 主键，课程编号     |
| pid           | Number | 1 | 分类的id     |
| name          | String   |        史蒂夫23路径               | 分类名字标题    |

#### 返回实例

```js
[
    {
        "id": 1,
        "pid": 0,
        "name": "童书"
    },
    {
        "id": 2,
        "pid": 0,
        "name": "文艺"
    },
    {
        "id": 3,
        "pid": 0,
        "name": "社科"
    },
    {
        "id": 4,
        "pid": 0,
        "name": "生活"
    },
    {
        "id": 5,
        "pid": 0,
        "name": "科技"
    },
    {
        "id": 6,
        "pid": 1,
        "name": "凯迪克奖获奖作品"
    },
    {
        "id": 7,
        "pid": 2,
        "name": "央视《朗读者》书单"
    },
    {
        "id": 17,
        "pid": 2,
        "name": "央视"
    },
    {
        "id": 8,
        "pid": 3,
        "name": "译文纪实系列书单"
    },
    {
        "id": 16,
        "pid": 3,
        "name": "翻译"
    },
    {
        "id": 9,
        "pid": 4,
        "name": "美食MOOK野路子"
    },
    {
        "id": 14,
        "pid": 4,
        "name": "野外生存美"
    },
    {
        "id": 10,
        "pid": 5,
        "name": "人民日报推荐"
    },
    {
        "id": 13,
        "pid": 5,
        "name": "童胡"
    },
    {
        "id": 11,
        "pid": 1,
        "name": "兴趣早读"
    },
    {
        "id": 12,
        "pid": 1,
        "name": "早教"
    },
    {
        "id": 15,
        "pid": 2,
        "name": "电子科学"
    }
]
```

## 教师端接口

### 获取教师端轮播图接口

教师端首页显示的轮播图列表

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/student/carousel` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是轮播图的数据。

```js
[{轮播图数据}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| order           | Number | 1 | 排序     |
| title          | String   |     美丽景色                  | 轮播图标题    |
| imgUrl        | String   | /a/b.png                 | 图片地址     |
| url         | String   | /home/a.html                       | 跳转地址    |

#### 返回实例

```js
// 获取成功返回的内容
[
    {
        "order": 1,
        "title": "美丽景色",
        "imgUrl": "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1555293675&di=a807c0f74255accb5380165976293a84&imgtype=jpg&er=1&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01398c5942618ca8012193a3f97976.jpg",
        "url": "http://www.aicoder.com"
    },
    {
        "order": 2,
        "title": "美丽景色1",
        "imgUrl": "http://www.33lc.com/article/UploadPic/2012-10/2012101714102663437.jpg",
        "url": "/login.html"
    },
    {
        "order": 3,
        "title": "美丽景色2",
        "imgUrl": "http://www.33lc.com/article/UploadPic/2012-10/2012101714103954400.jpg",
        "url": "/"
    }
]

// 未登录，返回失败消息，状态码是401
{
  code: 8,
  msg: '用户没有登录，不能访问'
}
```

### 获取教师端分类数据接口

课程分类数据：用于教材和课程。

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/teacher/course_category` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是推荐课程的数据。

```js
[{分类数据},{分类数据}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| id           | Number | 1 | 主键，课程编号     |
| pid           | Number | 1 | 分类的id     |
| name          | String   |        史蒂夫23路径               | 分类名字标题    |

#### 返回实例

```js
[
    {
        "id": 1,
        "pid": 0,
        "name": "童书"
    },
    {
        "id": 2,
        "pid": 0,
        "name": "文艺"
    },
    {
        "id": 3,
        "pid": 0,
        "name": "社科"
    },
    {
        "id": 4,
        "pid": 0,
        "name": "生活"
    },
    {
        "id": 5,
        "pid": 0,
        "name": "科技"
    },
    {
        "id": 6,
        "pid": 1,
        "name": "凯迪克奖获奖作品"
    },
    {
        "id": 7,
        "pid": 2,
        "name": "央视《朗读者》书单"
    },
    {
        "id": 17,
        "pid": 2,
        "name": "央视"
    },
    {
        "id": 8,
        "pid": 3,
        "name": "译文纪实系列书单"
    },
    {
        "id": 16,
        "pid": 3,
        "name": "翻译"
    },
    {
        "id": 9,
        "pid": 4,
        "name": "美食MOOK野路子"
    },
    {
        "id": 14,
        "pid": 4,
        "name": "野外生存美"
    },
    {
        "id": 10,
        "pid": 5,
        "name": "人民日报推荐"
    },
    {
        "id": 13,
        "pid": 5,
        "name": "童胡"
    },
    {
        "id": 11,
        "pid": 1,
        "name": "兴趣早读"
    },
    {
        "id": 12,
        "pid": 1,
        "name": "早教"
    },
    {
        "id": 15,
        "pid": 2,
        "name": "电子科学"
    }
]
```

### 获取教师端推荐教材

教师端首页推荐教材列表

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/teacher/materials?_limit=8&_order=id&isHot=true` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是推荐课程的数据。

```js
[{推荐教材数据1},{推荐教材数据2}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| id           | Number | 1 | 主键，课程编号     |
| catId           | Number | 1 | 分类的id     |
| title          | String   |        史蒂夫23路径               | 教材标题    |
| imgUrl        | String   | /a/b.png                 | 教材图片地址     |
| press         | String   | 清华出版社                     | 出版社    |
| deadline         | String   |     2019-04-09 10:13:21                 | 截止权限日期    |
| author         | String   |    李思              | 作者    |
| college         | String   |    清华大学              | 大学    |
| author         | String   |    李思              | 作者    |
| price         | String   |    30              | 价格    |
| description         | String   |    说明              | 教材内容说明    |
| ISBN         | String   |    000000000              | ISBN号    |
| author_des         | String   |    xx              | 作者介绍    |
| cat_des         | String   |                  | 分类说明    |
| isHot         | Boolean   |    true          | 是否热    |
| count         | Number   |    10          | 购买人数    |
| relevant_material         | Object   |              | 关联教材    |
| courseware_set         | Object   |              | 教材集    |
| question_bank         | Object   |              | 题库    |

#### 返回实例

```js
// 获取成功返回的内容
[
 {
    "id": 17,
    "catId": 8,
    "title": "产小何劳心社报米长",
    "imgUrl": "http://dummyimage.com/300/00405d/FFF&text=aicoder.com",
    "author": "张艳",
    "price": 41,
    "deadline": "2004-01-15 13:29:19",
    "relevant_material": [
        {
            "id": 54,
            "title": "求后物",
            "ISBN": "830000000002"
        },
        {
            "id": 13,
            "title": "示式往可",
            "ISBN": "830000000002"
        }
    ],
    "courseware_set": {
        "id": 10,
        "name": "构任小后",
        "count": 35
    },
    "question_bank": {
        "exercises": 467,
        "examination_paper": 269,
        "name": "气重段运"
    },
    "ISBN": "1000003200230",
    "description": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问</p>",
    "author_des": "<p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p>",
    "cat_des": "<p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p>",
    "isHot": true,
    "count": 127
  },
  {
    "id": 18,
    "catId": 14,
    "title": "导团可机意广们深打位况",
    "imgUrl": "http://dummyimage.com/300/00405d/FFF&text=aicoder.com",
    "author": "杜超",
    "price": 86,
    "deadline": "2009-08-18 02:24:47",
    "relevant_material": [
        {
            "id": 73,
            "title": "林何军于性",
            "ISBN": "830000000002"
        },
        {
            "id": 34,
            "title": "样只军七",
            "ISBN": "830000000002"
        }
    ],
    "courseware_set": {
        "id": 7,
        "name": "除再什",
        "count": 29
    },
    "question_bank": {
        "exercises": 797,
        "examination_paper": 123,
        "name": "加厂单动你法温"
    },
    "ISBN": "1000003200230",
    "description": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问</p>",
    "author_des": "<p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p><p>何直圆必格几定议到个军江北县。此问们把族引华华给何直圆必格几定议到个军江北县。此问们把族引华华给</p>",
    "cat_des": "<p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p><p>课程一： 是否连接历史角度发垃圾</p>",
    "isHot": true,
    "count": 60
  }
]

// 未登录，返回失败消息，状态码是401
{
  code: 8,
  msg: '用户没有登录，不能访问'
}
```

### 获取教师端推荐课程列表

教师端推荐课程列表

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/api/teacher/courses?_limit=8&_order=id&isHot=true` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |
| 特殊要求 | 携带登录后得到的token，不然会返回没有登录的消息 httpcode： 401             |

#### 请求参数

无

> 需要添加token密钥到header的Authorization中。

#### 返回值

后台返回一个数组，数组里面内容是推荐课程的数据。

```js
[{推荐教材数据1},{推荐教材数据2}]
```

| 属性            | 类型       | 参考值                      | 说明     |
|---------------|----------|--------------------------|--------|
| id           | Number | 1 | 主键，课程编号     |
| catId           | Number | 1 | 分类的id     |
| title          | String   |        史蒂夫23路径               | 课程标题    |
| img        | String   | /a/b.png                 | 课程图片地址 小图    |
| bgimg        | String   | /a/b.png                 | 课程图片地址 大图    |
| press         | String   | 清华出版社                     | 出版社    |
| subon         | String   |     2019-04-09 10:13:21                 | 发布日期    |
| author         | String   |    李思              | 作者    |
| college         | String   |    清华大学              | 大学    |
| author         | String   |    李思              | 作者    |
| price         | String   |    30              | 价格    |
| textbook         | String   |    说明              | 课程内容说明    |
| catalog         | String   |                  | 课程课时说明    |
| isHot         | Boolean   |    true          | 是否热    |
| isrecommend         | Boolean   |    true          | 是否推荐    |
| studycount         | Number   |    10          | 购买人数    |
| teacherId         | Number   |    10          | 所属教师    |
| invitecode         | String   |    10          | 邀请码    |
| studytime         | String   |    "2019-05-01 10:05:20"         | 开始学习时间    |

#### 返回实例

```js
[
  {
      "id": 1,
      "title": "间位特更战",
      "subon": "2019-04-09 10:13:21",
      "author": "邓艳",
      "college": "东南大学",
      "img": "http://dummyimage.com/183x160",
      "bgimg": "http://dummyimage.com/320x278",
      "press": "清华出版社",
      "price": 86,
      "textbook": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p>",
      "aboutauthor": "<p>韩少功，1953年出生于湖南长沙，祖籍湖南澧县 [1]  。著名作家。</p><p>曾获境内外奖项：1980年、1981年全国优秀短篇小说奖；2002年法国文化部颁发的“法兰西文艺骑士奖章”；2007年第五届华语文学传媒大奖之“杰出作家奖”；第四届鲁迅文学奖；美国第二届纽曼华语文学奖等。作品分别以十多种外国文字共三十多种在境外出版。另有译作《生命中不能承受之轻》（昆德拉著）、《惶然录》（佩索阿著）等数种出版</p>",
      "studycount": 137,
      "studytime": "2019.2.13-2019.12.30",
      "invitecode": "00293099",
      "catalog": "<p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p>",
      "isHot": true,
      "isrecommend": false,
      "catId": 16,
      "simimg": "http://dummyimage.com/185x160",
      "teacherId": 3
  },
  {
      "id": 2,
      "title": "属器权",
      "subon": "2019-04-09 10:13:21",
      "author": "石芳",
      "college": "东南大学",
      "img": "http://dummyimage.com/183x160",
      "bgimg": "http://dummyimage.com/320x278",
      "press": "清华出版社",
      "price": 96,
      "textbook": "<p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p><p>眼回何直圆必格几定议到个军江北县。此问们把族引华华给由者里龙外。划效线工年整制知共外华制明片影你金其。电称十结及完都系目新后看中无史。达界张共大交天示重方张切文。省积近西真商重不积力方节存。质受省但农还约我快江复市件流。团长山圆领斯圆就建条对包具。</p>",
      "aboutauthor": "<p>韩少功，1953年出生于湖南长沙，祖籍湖南澧县 [1]  。著名作家。</p><p>曾获境内外奖项：1980年、1981年全国优秀短篇小说奖；2002年法国文化部颁发的“法兰西文艺骑士奖章”；2007年第五届华语文学传媒大奖之“杰出作家奖”；第四届鲁迅文学奖；美国第二届纽曼华语文学奖等。作品分别以十多种外国文字共三十多种在境外出版。另有译作《生命中不能承受之轻》（昆德拉著）、《惶然录》（佩索阿著）等数种出版</p>",
      "studycount": 148,
      "studytime": "2019.2.13-2019.12.30",
      "invitecode": "00293099",
      "catalog": "<p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p><p>第一课时</p>",
      "isHot": true,
      "isrecommend": false,
      "catId": 10,
      "simimg": "http://dummyimage.com/185x160",
      "teacherId": 3
  }
]
```

## 权限相关

### 获取用户的所有权限

请求地址： http://192.168.1.130:8888/per/getUserPer/1003

获取用户的所有权限

| 类型   | 说明                                                   |
|------|------------------------------------------------------|
| 接口地址 | `http://192.168.1.130:8888/per/getUserPer/:id` |
| 请求方式 | `GET`                                               |
| 数据类型 | `application/x-www-form-urlencoded`                                   |

#### 请求参数

无

#### 返回值

后台返回一个数组，数组里面内容是用户的所有权限数据。

```js
[{权限1}]
```

#### 返回实例

```js
[
    {
        "id": 1004,
        "pId": 0,
        "type": "menu",
        "des": "矿生音",
        "status": 0,
        "del": 0,
        "subon": "2019-05-08 17:07:16",
        "subby": 1001,
        "code": 10004,
        "url": ""
    },
    {
        "id": 1014,
        "pId": 0,
        "type": "menu",
        "des": "即政或",
        "status": 0,
        "del": 0,
        "subon": "2019-05-08 17:07:16",
        "subby": 1001,
        "code": 10014,
        "url": ""
    }
]
```