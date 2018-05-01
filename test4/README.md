# 图书管理系统顺序图
---
## 1.借阅用例
### 1.1 PlantUML源代码：
@startuml<br>
hide footbox<br>
title 借阅图书顺序图<br>
actor 图书管理员 as user<br>
activate user<br>
user->图书馆书籍目录:获取图书目录<br>
activate 图书馆书籍目录<br>
图书馆书籍目录->图书:查找对应图书信息<br>
activate 图书<br>
deactivate 图书<br>
deactivate 图书馆书籍目录<br>
user->借阅记录:创建借阅记录<br>
activate 借阅记录<br>
deactivate 借阅记录<br>
user->图书馆书籍目录:书籍目录中书籍数量-1<br>
activate 图书馆书籍目录<br>
图书馆书籍目录->图书:可借数量-1<br>
activate 图书<br>
deactivate 图书<br>
deactivate 图书馆书籍目录<br>
user->读者:读者可借阅数量-1<br>
activate 读者<br>
deactivate 读者<br>

user->借阅记录:完成本次借阅操作<br>
activate 借阅记录<br>
deactivate 借阅记录<br>
@enduml

### 1.2 借阅用例顺序图
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test4/jieyueshunxutu.png)
---


## 2.还书用例
### 2.1 PlantUML源代码：
@startuml<br>
hide footbox<br>
title 归还图书顺序图<br>
actor 图书管理员 as user<br>
activate user<br>
activate 读者<br>

user->借书记录:查询借阅信息<br>
activate 借书记录<br>
借书记录->图书馆书籍目录:选中归还书籍目录<br>
activate 图书馆书籍目录<br>
图书馆书籍目录->图书:选中目标图书<br>
activate 图书<br>
deactivate 图书<br>
deactivate 图书馆书籍目录<br>
deactivate 借书记录<br>
user->读者:获取读者信息<br>
activate 读者<br>
读者->图书馆书籍目录:书籍目录信息+1<br>
activate 图书馆书籍目录<br>
图书馆书籍目录->图书:增加图书库存<br>
activate 图书<br>
图书->还书记录:增加还书记录<br>
activate 还书记录<br>
deactivate 还书记录<br>
deactivate 图书<br>
deactivate 图书馆书籍目录<br>
deactivate 读者<br>
user->读者:读者可借书籍+1<br>
activate 读者<br>
deactivate 读者<br>

@enduml

### 2.2 还书用例顺序图
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test4/guihuantushushunxutu.png)
---

## 3.个人信息修改用例顺序图

### 3.1 PlantUML源代码：

@startuml<br>
hide footbox<br>
title 修改个人信息顺序图<br>
actor 系统管理员 as user<br>
activate user<br>
user->读者:查询用户ID<br>
activate 读者<br>
读者->浏览器:进入个人主页<br>
activate 浏览器<br>
浏览器->服务器:请求数据<br>
activate 服务器<br>
服务器->数据库:获取读者个人信息<br>
activate 数据库<br>
deactivate 数据库<br>
deactivate 服务器<br>
deactivate 浏览器<br>
读者->浏览器:修改个人信息<br>
activate 浏览器<br>
浏览器->服务器:执行sql语句<br>
activate 服务器<br>
服务器->数据库:更新读者信息<br>
activate 数据库<br>
deactivate 数据库<br>
deactivate 服务器<br>
deactivate 浏览器<br>
deactivate 读者<br>
user->数据库:用户修改个人信息成功<br>
activate 数据库<br>
deactivate 数据库<br>
@enduml

### 3.2个人信息修改顺序图：
![Aaron Swartz](https://raw.githubusercontent.com/312922143/is_analysis/master/test4/gerenxinxixiugaishunxutu.png)
---