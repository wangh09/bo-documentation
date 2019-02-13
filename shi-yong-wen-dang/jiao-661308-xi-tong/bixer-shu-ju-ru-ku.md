## Bixer 数据导入

---

#### 1.jhi\_user 数据表

| jhi\_user | bixer 数据表 | bixer 对应字段 | jhi\_user格式 | bixer 数据格式 | 补充说明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **id** | identities 或者 members | id | bigint | int | **不确定使用哪一个主键** |
| email | identities | email | \*\*\*@\*\*.com | \*\*\*@\*\*.com |  |
| mobile | members | phone\_number | +86-13912341234 | 数据缺失 | **国家代码和手机号不隔离，无法正确发送短信** |
| lang\_key |  |  | **zh-CN / en-US** | 数据缺失 | **显示网站首页语种、短信、邮件语种** |
| password\_hash | identities | password\_digest | $2a$10$\*\*\*\*\* | $2a$10$\*\*\*\* | 密码算法一致 |
| ink\_id |  |  | inkId\_uuid |  | 可以补填 |
| activated | identities  | is\_active | boolean | tinyint | 数据一致 |
| first\_name |  |  |  |  | 非必填参数 |
| last\_name |  |  |  |  | 非必填参数 |
| image\_url |  |  |  |  | 非必填参数 |
| activation\_key |  |  |  |  | 非必填参数，激活使用 |
| reset\_key |  |  |  |  | 非必填参数，重置密码使用 |
| reset\_date |  |  |  |  | 非必填参数，重置密码使用 |
| ROLE\_FREEZE | identities 或者 members | is\_locked 或者 activated | 冻结用户权限 |  | 不确定是哪个字段 |

---

#### 2.kyc\_application 数据表

| kyc\_application | bixer 数据表 | bixer 对应字段 | kyc\_application 格式 | bixer 格式 | 补充说明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| user\_id | identities 或者 members | id | bigint | int | **不确定使用哪一个主键** |
| country\_code | members | country\_code | 86 | 数据缺失 | **需要明确数据格式，该字段决定 KYC 认证方式** |
| certificate\_level |  |  | normal | 数据缺失 | 可以统一补填为 normal |
| certificate\_status | id\_documents | aasm\_state | PASSED / PENDING / REJECETED | verifying | **bixer 几种状态未知，字段命名含义未知** |
| data |  |  | JSON |  |  |

#### data  所需 JSON 数据字段

| 支持字段 | bixer 数据表 | bixer 对应字段 | data 格式 | bixer 格式 | 补充说明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| fullName | id\_documents | name |  |  | 数据一致 |
| city | id\_documents | city | 北京 | Alexandria | 目前手动填写城市，数据可以匹配 |
| address | id\_documents | address | 海淀区 | Online St | 目前手动填写，数据可以匹配 |
| postalCode | id\_documents | zipcode | 100070 | \*\*\*\*\*\* | 目前手动填写，数据可以匹配 |
| givenName |  |  |  |  | 可选 |
| familyName |  |  |  |  | 可选 |
| front |  |  | key、url | 数据缺失 | **bixer 没有图片 key、url** |
| back |  |  | key、url | 数据缺失 | **同上** |
| handheld |  |  | key、url | 数据缺失 | **同上** |
| residenceProofTye | id\_documents | id\_documents\_type | bankStatement、taxBill、utilityBill、otherBill | 0 | **不清楚 bixer 的数据分别对应的是什么类型** |
| bankStatement |  |  | key、url | 数据缺失 | **bixer 没有图片key、url** |
| taxBill |  |  |  | 数据缺失 | **同上** |
| utilityBill |  |  |  | 数据缺失 | **同上** |
| otherBill |  |  |  | 数据缺失 | **同上** |

---

#### 3.security\_code 数据表

| security\_code | bixer 数据表 | bixer 对应字段 | security\_code 格式 | bixer 格式 | 补充说明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| user\_id | identities 或者 members | id | bigint | int | **不确定使用哪一个主键** |
| google\_secret | two\_factors | otp\_secret | totp 算法 | totp 算法 | **目前唯一的一条数据验证成功，仍需测试** |
| currency\_password |  |  | $2a$10$ | 数据缺失 | **bixer 缺失数据，资金密码使用和登录密码** |

---

#### 4. Bixer 只给了一个币种账户 Accounts 的表，别的信息都没有了。具体缺失什么，需要核对。



