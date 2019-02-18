# 前台展示

## 1. 使用方法说明

【补充】使用字典列表获取列表基本信息，具体内容使用文章内容获取。

## 2. 字典列表

#### 1.获取某一父节点下的子节点（权限开放）

```
GET    http://localhost:8082/ui/info/list?[type={type}&][parent={parent}&][language={language}]
```

* **参数说明：三个参数都不是必填，获取列表以 order 字段倒序排序展示（例：100在最前，1在最后）**

  * String  **type :  如果填必须是 tree \[ 如果该值填 tree ，将获得父节点下所有子节点 \] **
  * String  **parent : 父节点（类别）名称**
  * String  **language :** **语言必须使用下划线格式，例：zh\_CN**

* **前台部分展示示例**：

  * **轮播图：**parent = carousel
  * **公告详情：**parent = notice

* **类别说明：**

| parent | 涵义 |
| :--- | :--- |
| ex-footer-links | 首页底部链接。包括：关于我们（about-us），用户支持（customer-support）,帮助中心（help-center）,联系我们（contact-us），友情链接（frendship） |
| about-us | 关于我们。包括：公司简介\(company-profile\)，团队介绍\(team-intro\)，加入我们\(join-us\) |
| customer-support | 用户支持。包括：用户协议\(user-agreement\)，法律声明\(legal-notices\)，隐私条款\(privacy-policy\) |
| ex-carousel | 轮播图 |
| ex-login-modules | 登录模块。包括：注册配图（register），登录配图（login）,忘记密码配图（forgot-pass） |

* **返回结果：**

```
[
  {
    "parent": "about-us",
    "extension": "",
    "lastModifiedDate": null,
    "lastModifiedBy": "admin",
    "description": "公司简介",
    "language": "zh-CN",
    "url": "",
    "isShow": true,
    "imgUrl": "",
    "createdDate": "2018-10-24T07:04:40Z",
    "createdBy": "admin",
    "name": "company-profile",
    "id": 9,
    "order": 1
  },
  ......
]
```

**异常情况：无**

## 3. 文章内容

#### 1.按名称获取单个文章内容（权限开放）

```
GET    http://localhost:8082/ui/info/article/{dictName}/{language}
```

* **参数说明：**

  * String **dictName ：user-agreement / legal-notices / privacy-policy**
  * String **language ：zh-CN / en-US / ko-KR / ja-JP**

* **类别说明：**

| dictName | 说明 |
| :--- | :--- |
| user-agreement | 服务协议 |
| legal-notices | 隐私条款 |
| privacy-policy | 法律声明 |

* 返回结果：

```
{
  "id": 70,
  "dicId": 146,
  "title": "服务协议",
  "description": "服务协议",
  "extension": "服务协议",
  "content": "服务协议.......",
  "isShow": true,
  "language": "zh-CN",
  "orderBy": 0,
  "createdBy": "admin",
  "createdDate": "2018-08-13T10:44:53Z",
  "lastModifiedBy": "admin",
  "lastModifiedDate": "2018-08-13T10:44:53Z"
}
```

* **异常情况：无**

#### 2.按父名称获取文章标题列表（权限开放）

```
GET    http://localhost:8082/ui/info/list/article/{parent}/{language}?page={page}&size={size}&sort=[sort]
```

* **接口说明：**

  * **文章标题取  extension 的值**

* 参数说明：

  * String  **parent : notice**
  * String  **language ：zh-CN / en-US / ko-KR / ja-JP**
  * **Pageable ：**
    * Integer  **page : 0**
    * Integer  **size : 5**
    * Array** sort : id,desc**

* **返回结果：**

```
{
  "content": [
    {
      "id": 184,
      "parent": "notice",
      "name": "notice-new",
      "language": "zh-CN",
      "isShow": true,
      "url": null,
      "imgUrl": null,
      "status": 0,
      "orderBy": 0,
      "description": "项目公告",
      "extension": "项目公告",
      "createdBy": "admin",
      "createdDate": "2018-08-15T06:06:14Z",
      "lastModifiedBy": "admin",
      "lastModifiedDate": "2018-08-15T06:07:38Z"
    },
  ],
  "totalElements": 4,
  "totalPages": 1,
  "last": true,
  "size": 5,
  "number": 0,
  "sort": null,
  "first": true,
  "numberOfElements": 4
}
```

**异常情况：无**

