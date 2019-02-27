## 信息字典

| Parent | Name | Language | isShow | Url | ImgUrl | Status | OrderBy | Descripiton | Extension |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | ex-content | zh-CN | true |  |  |  |  | 内容设置 |  |
| root | ex-graphics | zh-CN | true |  |  |  |  | 配图设置 |  |
| root | ex-announcements | zh-CN | true |  |  |  |  | 公告 |  |
| ex-content | ex-menu-help | zh-CN | true |  |  |  |  | 帮助菜单 |  |
| ex-content | ex-footer-links | zh-CN | true |  |  |  |  | 首页底部链接 |  |
| ex-footer-links | about-us | zh-CN | true |  |  |  |  | 关于我们 |  |
| ex-footer-links | customer-support | zh-CN | true |  |  |  |  | 用户支持 |  |
| ex-footer-links | help-center | zh-CN | true |  |  |  |  | 帮助中心 |  |
| ex-footer-links | contract-us | zh-CN | true |  |  |  |  | 联系我们 |  |
| ex-footer-links | friendship | zh-CN | true |  |  |  |  | 友情链接 |  |
| ex-graphics | ex-carousel | zh-CN | true |  |  |  |  | 轮播图 |  |
| ex-graphics | ex-login-modules | zh-CN | true |  |  |  |  | 登录模块 |  |
| ex-login-modules | login | zh-CN | true |  |  |  |  | 登录配图 |  |
| ex-login-modules | register | zh-CN | true |  |  |  |  | 注册配图 |  |
| ex-login-modules | forgot-pass | zh-CN | true |  |  |  |  | 忘记密码配图 |  |
| about-us | company-profile | zh-CN | true |  |  |  |  | 公司简介 |  |
| about-us | team-intro | zh-CN | true |  |  |  |  | 团队简介 |  |
| about-us | join-us | zh-CN | true |  |  |  |  | 加入我们 |  |
| customer-support | user-agreement | zh-CN | true |  |  |  |  | 用户协议 |  |
| customer-support | legal-notices | zh-CN | true |  |  |  |  | 法律声明 |  |
| customer-support | privacy-policy | zh-CN | true |  |  |  |  | 隐私政策 |  |
| help-center | FAQ | zh-CN | true |  |  |  |  | 常见问题 |  |
| help-center | novice-guidance | zh-CN | true |  |  |  |  | 新手指导 |  |
| help-center | rate-standard | zh-CN | true |  |  |  |  | 费率标准 |  |

## 字段说明

* **parent 和 name 必须是英文，且多语种状态下都相同，并且 name 不允许同语种重复，否则添加时抛出500错误。**

| 字段 | 说明 | 是否必填 |
| :--- | :--- | :--- |
| **parent** | 父节点，查询子节点，输入该值 | ✅ |
| **name** | 子节点（同一语种不允许重复，具有唯一性） | ✅ |
| **language** | 语种，系统默认：中英日韩 | ✅ |
| **isShow** | 是否显示（是否为草稿状态） | ✅ |
| **url** | 轮播图 url | ❌ |
| **imgUrl** | 轮播图跳转链接 | ❌ |
| **status** | 备用字段 | ❌ |
| **orderBy** | 排序（默认降序） | ✅ |
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
| **orderBy** | **排序（默认降序）** | ✅ |



