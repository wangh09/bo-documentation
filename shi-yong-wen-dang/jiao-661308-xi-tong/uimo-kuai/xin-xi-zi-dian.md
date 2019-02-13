## 信息字典

| Parent | Name | Language | isShow | Url | ImgUrl | Status | OrderBy | Descripiton | Extension |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | about | zh-CN | true |  |  |  |  | 关于我们 |  |
| root | friendship | zh-CN | true |  |  |  |  | 友情链接 |  |
| root | support | zh-CN | true |  |  |  |  | 用户支持 |  |
| root | carousel | zh-CN | true |  |  |  |  | 首页轮播图 |  |
| root | help-center | zh-CN | true |  |  |  |  | 帮助中心 |  |
| root | follow-us | zh-CN | true |  |  |  |  | 关注我们 |  |
| root | website-config | zh-CN | true |  |  |  |  | 网站配图 |  |
| about | company-profile | zh-CN | true |  |  |  |  | 公司简介 |  |
| about | team-intro | zh-CN | true |  |  |  |  | 团队简介 |  |
| about | join-us | zh-CN | true |  |  |  |  | 加入我们 |  |
| support | user-agreement | zh-CN | true |  |  |  |  | 用户协议 |  |
| support | legal-notices | zh-CN | true |  |  |  |  | 法律声明 |  |
| support | privacy-policy | zh-CN | true |  |  |  |  | 隐私政策 |  |
| help-center | create-api | zh-CN | true |  |  |  |  | 创建 API |  |
| help-center | rate-standard | zh-CN | true |  |  |  |  | 费率标准 |  |
| help-center | novice-guidance | zh-CN | true |  |  |  |  | 新手指导 |  |
| help-center | FAQ | zh-CN | true |  |  |  |  | 常见问题 |  |
| help-center | business-cooperation | zh-CN | true |  |  |  |  | 商务合作 |  |
| follow-us | Facebook | zh-CN | true |  |  |  |  | 脸书 |  |
| follow-us | Twitter | zh-CN | true |  |  |  |  | 推特 |  |
| follow-us | WeChat | zh-CN | true |  |  |  |  | 微信 |  |
| follow-us | Weibo | zh-CN | true |  |  |  |  | 微博 |  |

## 字段说明

* **parent 和 name 必须是英文，且多语种状态下都相同，并且 name 不允许同语种重复，否则添加时抛出500错误。**

| 字段 | 说明 | 是否必填 |
| :--- | :--- | :--- |
| **parent** | 父节点，查询子节点，输入该值 | ✅ |
| **name** | 子节点 | ✅ |
| **language** | 语种，系统默认：中英日韩 | ✅ |
| **isShow** | 是否显示（是否为草稿状态） | ✅ |
| **url** | 轮播图 url | ❌ |
| **imgUrl** | 轮播图跳转链接 | ❌ |
| **status** | 备用字段 | ❌ |
| **orderBy** | 排序 | ✅ |
| **description** | 描述 | ✅ |
| **extension** | **目前公告存储标题（公告详情展示时，不需要查询 content 表）、轮播图存储图片名字** | ❌ |

## 内容表

#### （ 字典 One &lt;--&gt;  内容 One ）,数据库不允许一个 dictionary 的主键 id ，对应多个 content 。

| 字段 | 说明 | 是否必填 |
| :--- | :--- | :--- |
| **dicId** | **字典主键（dicId在内容表具有唯一性）** | ✅ |
| **uniqueId** | **同一内容的多语种文章相同，查看，更新，删除文章时必须传入相同的值** | ✅（更新必填，创建时不需要） |
| **title** | **文章标题，添加公告详情时，需要把 title 的值回填到字典的 descriptiion，应用场景：前端展示公告详情时，不需要查询内容部获取 title.** | ✅ |
| **description** | 文章描述 | ❌（建议填写） |
| **extension** | 备用扩展字段。 | ❌ |
| **content** | **文章内容** | ✅ |
| **isShow** | **是否显示（是否为草稿），管理后台需要根据该字段显示不同状态。** | ✅ |
| **language** | 语种 | ✅ |
| **orderBy** | **排序** | ✅ |



