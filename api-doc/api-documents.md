  
# INK-EX API DOCUMENTS    
##  基本模块介绍  
  
1. 注册模块  
  
>     1.1 检查邮箱是否存在  
>     1.2 发送邮箱验证码  
>     1.3 校验邮箱验证码  
>     1.4 生成图形验证码 
>     1.5 校验图形验证码  
>     1.6 注册用户  

2. 登录模块  
  
>      2.1 用户鉴权，获取访问权限  
>      2.2 获取用户绑定的信息（是否绑定手机、GA，确定登录流程）  
>      2.3 发送短信登录验证码  
>      2.4 校验短信登录验证码  
>      2.5 校验 GA 验证码  
>      2.6 登录获取用户信息  

  3. 个人中心模块  
  
>      3.1 基本用户信息  
>           3.1.1 展示用户邮箱、手机号码信息  
>           3.1.2 用户 KYC 信息显示 （UI模块增加）  
>           3.1.3 用户登录历史 （只显示10条数据）  
  >      3.2 安全设置  
>          3.2.1 修改登录密码  
>          3.2.2 绑定手机号码  
>          3.2.3 绑定 GA  
>          3.2.4 设置资金安全密码  
  
## 注册模块  
  ### 检查用户注册邮箱是否存在   
 - GET  http://47.92.88.235:8082/auth/email/check/{email}    
  - Param: String  `email`  
 - Return: `true / false `   
 ### 发送邮箱验证码  
  - GET http://47.92.88.235:8082/auth/email/login-code/send/{email}/{language}  
  - Param: String  `email`  
 - Param: String  `language`  
 - Return: void     
       
### 校验邮箱验证码  
- GET http://47.92.88.235:8082/auth/email/login-code/verify/{email}/{key}  
  - Param: String  `email`  
 - Param: String  `key`  
 - Return: `true / false`  
 - 
### 生成图形验证码 [ 放入 img  标签 ]    

- GET http://47.92.88.235:8082/graphical/code

### 校验图形验证码 

- POST http://47.92.88.235:8082/graphical/verify
```
	{
		"graphicalContent":"11234"
	}
```

### 创建用户  
```
    Email Regex :  \\w+@\\w+\\.[a-z]+(\\.[a-z]+)?   
    Password strategy：                     
    1234 ❌    
    4321 ❌   
    abcd ❌   
    dcba ❌   
	number/word(8) ⭐️    
	number/word(8-16) ⭐️⭐️    
	number+word(8) ⭐️⭐️⭐️    
	number+word+symbol（8-16） ⭐️⭐️⭐️⭐️    
	number+symbol+word+symbol（8-16） ⭐️⭐️⭐️⭐️⭐️   
``` 
   
- POST http://47.92.88.235:8082/auth/user/register    
        
   - 注册调用参数示例：  

```             
          {  
			"email":"admin@localhost.com", 
			"activateKey":"57203639045617618339", 
			"password":"123456", 
			"langKey":"zh-cn" 
		  }
 ```
  - Exception:     
      - 400   the password is incorrect    
      - 400   the email is already used    
    
--- 

## 登录模块  

  ### 邮箱 / 手机 登录  
  
  #### 使用  用户邮箱 / 手机号码 获取访问权限  
  
  - POST http://47.92.88.235:8082/authenticate/login    
  
   - 调用示例  ParamType:  application/json    
``` 
         {    
          "username":"admin@localhost.com", / "+86-10010"   
          "password":"admin",   
          "rememberMe":"false"  
         }  
 ```    
   - Return:    
     - 用户名和密码正确时：  
    
```
		{    
             "access_token": "eyJhbGciOiJSUzI1NiIs .............",   
             "token_type": "bearer",   
             "refresh_token": "eyJhbGciOiJSU..........",   
             "expires_in": 298,   
             "scope": "openid",   
             "userId": 3,   
             "inkId": "1010",   
             "iat": 1528968951,   
             "jti": "9dd2dc7e-7889-4f45-b2a7-64119f8c2c32"   
         }    
```   

 - 用户名或密码错误时：    
         
         - title: Internal Server Error    
         - status: 500     
         - detail: 400 Bad Request    
          
### 获取用户绑定信息 [ 确定用户使用哪种登录逻辑 ]    
 - GET http://47.92.88.235:8082/auth/secure/bind/info    
- Return:    
  - mobile    
     - `true / false   `  
 - googleSecret    
     - `true / false   `  
 - currencyPassword    
     - `true / false  `  

### 生成图形验证码 [ 放入 img  标签 ]    

- GET http://47.92.88.235:8082/graphical/code

### 校验图形验证码 

- POST http://47.92.88.235:8082/graphical/verify
```
	{
		"graphicalContent":"11234"
	}
```

 ### 发送短信验登录证码   
 - GET http://47.92.88.235:8082/authenticate/sms/login-code/send/{mobile}  
   - Param: String mobile [ +86-138******** ]    
- Return:    
     - String `send_sms_success`  
 - String `send_sms_failed`  
  ### 校验短信登录验证码  
  - GET  http://47.92.88.235:8082/authenticate/sms/login-code/verify/{mobile}/{authCode}  
   - Param: String `mobile` [ +86-138******** ]    
- Param: String `authCode` [ 987123 ]    
- Return:    
     - String `check_success`  
	 - String `check_failed`  
	 - String `check_notExists`  
  ### 校验 GA 验证码  
  
- GET http://47.92.88.235:8082/auth/secure/ga/verify/{gaCode}    
   - Param: String `gaCode`  
  - Return:    
     - Boolean `true / false  `  
  ### 当获取登录权限，进行登录获取用户信息   
- GET http://47.92.88.235:8082/auth/user/current    
     
   - Return:    

```              
      {    
             "id": 3,  
			 "email": "admin@localhost.com",              
			 "mobile": "+86-10010",   
             "inkId": "1010",   
             "areaCode": "+86",   
             "firstName": "Administrator",   
             "lastName": "Administrator",   
             "imageUrl": "",    
             "activated": true,   
             "langKey": "en",   
             "createdBy": "system",   
             "createdDate": "2018-06-11T13:56:52Z",   
             "lastModifiedBy": "system",   
             "lastModifiedDate": null,   
             "authorities": [ "ROLE_USER", "ROLE_ADMIN" ]   
       }  
```
              
  - Exception:    
     - 500 (Internal Server Error) if the user couldn't be returned    
       
----    
 ## 用户中心    
 ### 基本用户信息   
 ####  获取用户基本信息，展示邮箱号码、手机号码（加*显示）   
 - GET http://47.92.88.235:8082/auth/user/info    
   - Return:    

```       
   {    
          "id": 3,   
          "email": "admin@localhost.com",   
          "mobile": "+86-10010",   
          "inkId": "1010",   
          "areaCode": "+86",   
          "firstName": "Administrator",   
          "lastName": "Administrator",   
          "imageUrl": "",   
          "activated": true,   
          "langKey": "en",   
          "createdBy": "system",   
          "createdDate": "2018-06-11T13:56:52Z",   
          "lastModifiedBy": "system",   
          "lastModifiedDate": null,   
          "authorities": [ "ROLE_USER", "ROLE_ADMIN" ]   
   }  
```

  - Exception:    
     - 500 (Internal Server Error) if the user couldn't be returned    
       
#### 用户 KYC 信息展示  
  - Need To Be Add    
    
#### 用户登录历史  
  - GET http://47.92.88.235:8082/auth/user/login-logs    
  
	   - Return:    
    
```          
         [     
            {     
               "id": 1,     
               "userId": "3",     
               "ipAddress": "192.168.0.1",     
               "countryName": "CHINA",    
              "cityName": "Beijing",               
              "status": "success",     
               "createdBy": "system",    
               "createdDate": "2018-06-11T13:56:52Z",              
                "lastModifiedBy": "system",     
                "lastModifiedDate": null,    
           }, {     
               "id": 2,     
               "userId": "3",     
               "ipAddress": "192.168.0.2",     
               "countryName": "CHINA",    
              "cityName": "Beijing",               
              "status": "success",     
               "createdBy": "system",    
              "createdDate": "2018-06-11T13:56:52Z",              
              "lastModifiedBy": "system",     
               "lastModifiedDate": null,    
             },            
             ........    
		]   
```

#### 安全设置  
 - 修改登录密码 [ 使用该 API 可能需要获取用户绑定信息，调用校验逻辑 ]   
 - POST http://47.92.88.235:8082/auth/user//change-old-password 
	 - 调用示例：
```
	{
		"oldPassword":"123456",
		"newPassword":"234567"
	}
```
 
- Exception:     
       - 400 (Bad Request) if the new password is incorrect    
  
- 绑定手机号码   
  - POST http://47.92.88.235:8082/auth/user/mobile    
    - Param:    
   
```             
       {    
             "firstName": "string",   
             "imageUrl": "string",   
             "langKey": "string",         [ en/cn ]   
             "lastName": "string",   
             "mobile": "string",          [ +86-138******** ]   
             "areaCode": "string"          [ +86 ]   
		}   
```

- Exception:    
         - 400 (Bad Request) if the mobile is already used    
         - 500 (Internal Server Error) if the user login wasn't found    
  
- 绑定 GA  
  
  - POST http://47.92.88.235:8082/auth/secure/ga   
       
    - Return:    

```			          
     {    
             "createdBy": "me-haha",   
             "createdDate": "2018-06-14T08:14:44.116Z",   
             "currencyPassword":  null,         [ 资金密码必须为 null ]   
             "googleSecret": "LPTPP6QOR62A6COU",                
             "id": 1,    
             "lastModifiedBy": "me-haha",   
             "lastModifiedDate": "2018-06-14T08:14:44.116Z",   
             "userId": 0   
      }    
        
```
        
 - Exception:    
         - 500 (Internal Server Error) if the user login wasn't found    
         - 400 (Bad Request) if the user id already exists    

- 获取 GA  
  
  - GET http://47.92.88.235:8082/auth/secure/ga
  - Return: 
  ```
  {    
             "createdBy": "me-haha",   
             "createdDate": "2018-06-14T08:14:44.116Z",   
             "currencyPassword":  null,         [ 资金密码必须为 null ]   
             "googleSecret": "LPTPP6QOR62A6COU",                
             "id": 1,    
             "lastModifiedBy": "me-haha",   
             "lastModifiedDate": "2018-06-14T08:14:44.116Z",   
             "userId": 0   
      }
  ```
           
- 设置 资金安全密码  
  
  - POST http://47.92.88.235:8082/auth/secure/currency-password/{currencyPassword}   
    - Param:  String `currencyPassword`  
  - Exception:    
      - 500 (Internal Server Error) if the user login wasn't found     
      
- 重置 资金安全密码  

	- POST http://47.92.88.235:8082/auth/secure/change-old-currency-password

```
	{
		"oldCurrencyPassword":"123456",
		"newCurrencyPassword":"234567"
	}
```

- Exception:    
	- 500 (Internal Server Error) if the user login wasn't found     

- 交易按照用户选择免安全资金密码输入 （Need to be add)    
  - every time    
  - every hour    
  - 24 hour