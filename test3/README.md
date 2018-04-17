# 1.图书管理系统的类图
---
### 1.1类图UML源码如下：

@startuml
class 读者{<br>
学号<br>
年龄<br>
性别<br>
电话<br>
专业<br>
学院<br>
邮箱<br>
已借阅书籍<br>
登录时间<br>
家庭地址<br>
}<br>

class 图书管理员{<br>
编号<br>
姓名<br>
年龄<br>
性别<br>
电话<br>
邮箱<br>
家庭地址<br>
}<br>

class 账号信息{<br>
编号<br>
账号<br>
密码<br>
用户权限<br>
}<br>

class 图书{<br>
编号<br>
名字<br>
价格<br>
出版社<br>
出版时间<br>
库存<br>
已借出数量<br>
ISBN号<br>
简介<br>
}<br>

class 借阅表{<br>
编号<br>
借书人编号<br>
图书编号<br>
借阅时间<br>
归还时间<br>
违约期限<br>
是否按时归还<br>
处理人编号<br>
}<br>

class 违约罚款{<br>
编号<br>
罚款人编号<br>
图书编号<br>
罚款原因<br>
罚款金额<br>
处理人编号<br>
罚款时间<br>
}<br>

图书管理员"1" --"n"读者<br>
图书"n"--"1"读者<br>
借阅表"1"--"1"读者<br>
账号信息"1"--"1"读者<br>
账号信息"1"--"1"图书管理员<br>
违约罚款"1"--"1"读者<br>
违约罚款"n"--"1"图书管理员<br>

@enduml

---

### 1.2 类图如下：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test3/shitu.png)

---

#2.图书管理系统的对象图
---
###2.1类读者对象图

####源码：

object 读者 {<br>
学号=201510414423<br>
姓名=杨青鹏<br>
年龄=22<br>
性别=1        (0:女 1:男）<br>
电话=18380277133<br>
专业=软件工程<br>
学院=信息科学与工程<br>
邮箱=312922144@qq.com<br>
已借阅图书数量=13<br>
可借图书量=2<br>
上次登录时间=2015-02-03 15:25:41<br>
家庭地址四川成都<br>
}<br>

####对象图：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test3/duzhe.png)
---
###2.2类图书管理员对象图

####源码：

object 图书管理员 {<br>
编号=5101000102<br>
姓名=张奇<br>
年龄=22<br>
性别=1        (0:女 1:男）<br>
电话=1583247898<br>
邮箱=zq@163.com<br>
家庭地址=四川成都<br>
}<br>
####对象图：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test3/tushuguanliyuan.png)
---
###2.3类账号对象图

####源码：

object 账号 {<br>
编号=5101007777<br>
账号=1815498447<br>
密码=12345679<br>
角色=1      (1:管理员 0:学生)<br>
}<br>

####对象图：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test3/zhanghao.png)
---
###2.4类图书对象图

####源码：

object 图书 {<br>
编号=5101000115<br>
名字=疯狂java<br>
价格=54.5<br>
出版社=清华大学出版社<br>
出版时间=2015-02-03 15:25:41<br>
可借阅量=2<br>
已借阅量=25<br>
总借阅次数=2<br>
ISBN号=978-7-302-32982-4<br>
简介=简介内容(长度大于等于0)<br>
}<br>
####对象图：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test3/tushu.png)
---
###2.5类借阅表对象图

####源码：

object 借阅表 {<br>
编号=5101008718<br>
借书人编号=5101000999<br>
图书编号=5101000115<br>
借阅时间=2015-02-03 15:25:41<br>
规定还书时间=2015-02-31 15:25:41<br>
实际还书时间=2015-02-09 15:25:41<br>
是否超期=0    (1:超期 0:未超期)<br>
处理人编号=14949916215<br>
罚款编号=14949916166xx26215<br>
}<br>
####对象图：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test3/jieyuebiao.png)
---
###2.6类罚款对象图

####源码：

object 罚款 {<br>
编号=9549497949594<br>
罚款者编号=9549497949594142<br>
图书编号 =5101000115<br>
罚款原因=超期一天<br>
罚款金额=80<br>
处理人编号=5101008715<br>
罚款时间=2015-02-09 15:25:41<br>
}<br>

####对象图：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test3/fakuan.png)