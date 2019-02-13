#### 1.获取某一父节点下的子节点（权限开放）

```
GET    http://localhost:8080/web-server/info/dict/node?[type={type}&][parent={parent}&][language={language}]
```

* **参数说明：三个参数都不是必填**

  * String  **type :  如果填必须是 tree \[ 如果该值填 tree ，将获得父节点下所有子节点 \] **
  * String  **parent : 父节点（类别）名称**
  * String  **language : zh\_CN / en\_US / ko\_KR / ja\_JP  语言必须使用下划线格式**

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

#### 2.添加 / 更新 字典（文章）

```
POST    http://localhost:8080/web-server/info/dict
```

* **接口主要应用场景：**

  * **创建 / 更新字典。比如：关于我们、用户支持、友情链接等。**
  * **创建 / 更新字典和文章。比如：网站的公告详情。**

* **接口使用：如只创建字典数据，内容数据不填。默认中英日韩四种语言。**

  * **Dictionary：**

    * **parent、name 作为节点，必须是英文，且多语种内 parent 、name 必须相同。但是同一语种内必须具有唯一性，否则 500 错误。**

    * **如果添加的是公告详情，Dictionary 的 extension 字段需要存储 Content 的 title 字段，方便前台页面展示公告列表详情的标题。**

    * **如果添加的是 Carousel 子节点，则需要把上传轮播图的 Key（图片名字）存储到 extension 字段。**

    * **如果添加的是 website-config 的子节点，用来配置网站注册、登录、修改密码的图片，则需要在 website-config 下新建三个子节点，比如：register、login、changePass，然后分别在刚在新建的三个节点下新建后缀为 Image 的节点，将图片 url 存入，并将 Key（图片名字）存储到 extension 字段，如果需要设置背景色，则在该字段做冗余处理。**

    * **parent、name、language、isShow、order、description、**

  * **Content：**

    * **title、content、isShow、language、order 必填字段**

  * **更新：**

    * **Dictionary：**

      * **id 补填**

    * **Content：**

      * **id 补填**

      * **dicId 补填**

      * **uniqueId 补填 （同一文字多语种拥有相同的 uniqueId）**

* **参数说明：注意 Json \[ \] 内字段为更新补填**

```
[
    {
        "dictionary": {
            ["id": 100,]
            "parent": "notice",
            "name": "tokenNotice",
            "language": "zh-CN",
            "isShow": true,
            "url": null,
            "imgUrl": null,
            "status": 0,
            "order": 1,
            "show": true,
            "description": "公告详情-上币公告",
            "extension": "上币公告"
        },
        "content": {
            ["id": 110,]
            ["dicId": 100,]
            ["uniqueId": "***************"]
            "title": "上币公告",
            "content": "***************",
            "language": "zh-CN",
            "isShow": true,
            "order": 1,
            "description": "上币公告中文说明",
            "extension": null
        }
    },
    .....[en-US]、[ko-KR]、[ja-JP]
]
```

* **返回结果：**

```
[
    {
        "dictionary": {
            "id": 100,
            "parent": "notice",
            "name": "tokenNotice",
            "language": "zh-CN",
            "isShow": true,
            "url": null,
            "imgUrl": null,
            "status": 0,
            "order": 1,
            "show": true,
            "description": "公告详情-上币公告",
            "extension": "上币公告",
            "createdBy": "anonymousUser",
            "createdDate": "2018-10-27T16:59:10.114Z",
            "lastModifiedBy": "anonymousUser",
            "lastModifiedDate": "2018-10-27T16:59:10.114Z",
        },
        "content": {
            "id": 110,
            "dicId": 100,
            "uniqueId": "cd1b93b2a90a424f947fb352f774ac3d"
            "title": "上币公告",
            "content": "***************",
            "language": "zh-CN",
            "isShow": true,
            "order": 1,
            "description": "上币公告中文说明",
            "extension": null,
            "createdBy": "anonymousUser",
            "createdDate": "2018-10-27T16:59:10.114Z",
            "lastModifiedBy": "anonymousUser",
            "lastModifiedDate": "2018-10-27T16:59:10.114Z",
        }
    },
    .....[en-US]、[ko-KR]、[ja-JP]
]
```

* **异常情况：**
  * **426  Dictionary 的 name 同一语种不具有唯一（UI 模块 426 异常）**
  * **424  Content 的 dicId 在新建时，已经重复。保证一个字典节点对应一篇文章（UI 模块 400 异常）**



