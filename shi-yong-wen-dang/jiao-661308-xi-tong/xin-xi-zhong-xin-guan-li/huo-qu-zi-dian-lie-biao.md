## 字典列表

#### 1.获取某一父节点下的子节点（权限开放）

```
GET    http://localhost:8080/web-server/info/dict/node?[type={type}&][parent={parent}&][language={language}]
```

* **参数说明：三个参数都不是必填，获取列表以 order 字段倒序排序展示（例：100在最前，1在最后）**

  * String  **type :  如果填必须是 tree \[ 如果该值填 tree ，将获得父节点下所有子节点 \] **
  * String  **parent : 父节点（类别）名称**
  * String  **language : 语言必须使用下划线格式，例：zh\_CN**

* **前台部分展示示例**：

  * **轮播图：**parent = carousel
  * **公告详情：**parent = notice

* **类别说明：**

| parent | 涵义 |
| :--- | :--- |
| about | 关于我们。包括：公司简介\(company-profile\)，团队介绍\(team-intro\)，加入我们\(join-us\) |
| support | 用户支持。包括：用户协议\(user-agreement\)，法律声明\(legal-notices\)，隐私条款\(privacy-policy\) |
| follow-us | 关注我们 |
| friendship | 友情链接 |
| carousel | 首页轮播图 |
| website-config | 网站配图。包括：注册、登录、修改密码页面配图 |

* **返回结果：**

```
[
  {
    "parent": "about",
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

