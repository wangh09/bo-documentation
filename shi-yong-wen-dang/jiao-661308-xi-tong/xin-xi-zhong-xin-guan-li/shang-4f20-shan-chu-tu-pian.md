#### 1.上传多语种图片

```
POST    http://localhost:8080/web-server/oss/upload/{type}/
```

* **接口说明：**
* **参数说明：**
  * String **type：**
    * **banner  网站前台轮播图**
    * **licence  用户 KYC 照片**
    * **login  网站前台登录配图**
    * **changePass  网站前台修改密码配图**
    * **register  网站前台用户注册配图**
    * **symbol  网站前台币种 logo**
    * **token 网站赠币文件（用来保存收到该增币活动用户的快照）**
  * **MultiFileVM（多语种文件）**
    * MultiFile fileCN
    * MultiFile fileEN
    * MultiFile fileKR
    * MultiFile fileJP
* **返回结果：**

```
{
    "ossCN": {
        "name": "efc03403c51943a6b129dca7c5f01b51.svg",
        "address": "//s3.ap-southeast-1.amazonaws.com/chinaexchange/manager/banner/efc03403c51943a6b129dca7c5f01b51.svg"
    },
    "ossEN": {
        "name": "0fb85e5414f5462aba76ebf6abce1389.svg",
        "address": "//s3.ap-southeast-1.amazonaws.com/chinaexchange/manager/banner/0fb85e5414f5462aba76ebf6abce1389.svg"
    },
    "ossJP": {
        "name": "878f00bf50f040e8a8697aa0a7eab880.svg",
        "address": "//s3.ap-southeast-1.amazonaws.com/chinaexchange/manager/banner/878f00bf50f040e8a8697aa0a7eab880.svg"
    },
    "ossKR": {
        "name": "213eaf7aa04945edb465c43a82de79cd.svg",
        "address": "//s3.ap-southeast-1.amazonaws.com/chinaexchange/manager/banner/213eaf7aa04945edb465c43a82de79cd.svg"
    }
}
```

* **异常情况：无**

---

#### 2.删除图片

```
DELETE     http://localhost:8080/web-server/oss/{type}/{name}
```

* **参数说明：**
  * String **type：参考上边 type  **
  * String **name：图片名字**
* **返回结果：无**
* **异常情况：无**



