## 基于GitHub的实验管理平台的分析与设计
---
### 1.概述：
老师操作功能：<br>
1.登录系统进行个人信息的修改和密码修改<br>
2.查询自己教授学生的信息列表<br>
3.对学生成绩进行评分<br>

学生操作功能：<br>
1.登录系统进行个人信息的修改和密码修改<br>
2.查询自己的实验成绩<br>

### 2.系统结构图：
![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My2.png)
<br>
### 3.用例设计：
![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My.png)
<br>
源码：
@startuml<br>
left to right direction<br>
skinparam packageStyle rectangle<br>
:教师: as Teacher<br>
:学生: as Student<br>
rectangle 用例 {<br>

(登出)  <--- Student<br>
(个人信息查询) <--- Student<br>
(登录)<--- Student<br>
(密码修改) <--- Student<br>
(个人信息修改)<--Student<br>
(成绩查询) <-- Student<br>
(选课) <-- Student<br>

Teacher --> (登出)<br>
Teacher --> (个人信息查询)<br>
Teacher --> (个人信息修改)<br>
Teacher --> (密码修改)<br>
Teacher --> (登录)<br>
Teacher --> (成绩评定)<br>
Teacher --> (学生信息列表查询)<br>
Teacher --> (成绩查询)<br>
Teacher --> (选课)<br>

(个人信息查询)  .> (登录) : include<br>
(密码修改)  .> (登录) : include<br>
(个人信息修改).>(登录) : include<br>
(成绩评定).>(登录):include<br>
(学生信息列表查询).>(登录):include<br>
(登出).>(登录):include<br>
(成绩查询).>(登录):include<br>
(选课).>(登录):include<br>
}
@enduml
### 4.类图：
![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My13.png)
<br>
源码：<br>
@startuml<br>
class Academy{<br>
 id  学院ID值<br>
 name 学院名字<br>
 universityId  学校的Id值<br>
 }<br>

class Account{<br>
id  账号的主键Id值<br>
universityId  学校表的Id值<br>
account  登录账号<br>
password  密码MD5加密<br>
role  角色分类<br>
value  是否可用<br>
}<br>

class Student {<br>
id  学生信息主键<br>
studentNo  学号<br>
accountId  账号表的Id值<br>
name  学生姓名<br>
gender  性别<br>
age  年龄<br>
classId 所属班级Id值<br>
academyId 学院ID<br>
idcard 身份证号<br>
major 专业<br>
}<br>

class Teacher{<br>
id Id值<br>
accountId 账号表的Id值<br>
teacherNo 教师编号<br>
name 姓名<br>
gender 性别<br>
gender 年龄<br>
position 职称<br>
degree 学历<br>
idcard 身份证号<br>
}<br>

class Course{<br>
id 课程的Id值<br>
code 课程代码<br>
name 课程名字<br>
term 学期<br>
academyId 学院ID<br>
grade 年级<br>
studentsId 该学科专业学生合集<br>
teacherIds 该学科教师合集<br>
}<br>


class Teacher_Course_Student{<br>
id Id值<br>
teacherId 教师Id值<br>
studentId 学生Id值<br>
courseId 课程Id值<br>
startTime 开课时间<br>
totalTestScore 实验总分<br>
}<br>

class Test{<br>
id 实验Id值<br>
name 实验名字<br>
issuetime 发布的时间<br>
desc 实验描述<br>
courseId 课程Id值<br>
}<br>
class TestSub{<br>
id  Id值<br>
limitScore 最高可得分<br>
kind  评分项<br>
testId 实验Id值<br>
}<br>
class TestScore{<br>
id Id值<br>
score 实验得分<br>
number 第几次实验<br>
time 评分日期<br>
courseId 课程Id值<br>
studentId 学生Id值<br>
}<br>
class TestSub_TestScore{<br>
id Id值<br>
trueScore 实际得分<br>
mark 评语<br>
testSubId 小评分项的Id值<br>
testScoreId 某次实验得分的Id值<br>
}<br>

Academy "*" --"1"  University<br>
Account "*"  -- "1"  University<br>
Account "1" -- "1" Student<br>
Account "1" -- "1" Teacher<br>
Class "1" -- "*" Student<br>

Teacher_Course_Student "1" -- "1" Student<br>
Teacher_Course_Student "*" -- "1" Teacher<br>
Teacher_Course_Student "*" -- "1" Course<br>
Test "*" --"1" Course<br>
TestSub "*" --"1" Test<br>
Student "1"--"*" TestScore<br>
TestScore "*" --"1" Course<br>
TestSub_TestScore "*" --"1" TestScore<br>
TestSub_TestScore "1" --"1" TestSub<br>


@enduml<br>
### 5.数据库设计：
#### 1. University(学校)
<table cellspacing="0" id="university">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>可以为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>为自增</td>
	<td>主键</td>
</tr>
<tr>
	<td>name</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>学校名</td>
</tr>
<tr>
	<td>location</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td>详细的地址</td>
	<td>学校地址</td>
</tr>
<tr>
	<td>level</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>一本/二本/专科</td>
</tr>
</table>

#### 2. Academy(学院)
<table cellspacing="0" id="academy">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>可以为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值是自增</td>
	<td>主键</td>
</tr>
<tr>
	<td>universityId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为学校表的主键</td>
	<td>学校的ID号</td>
</tr>
<tr>
	<td>name</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>学院名</td>
</tr>
</table>

#### 3. Account(账号)

<table cellspacing="0" id="account">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>可以为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值为自增</td>
	<td>主键</td>
</tr>
<tr>
	<td>universityId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值为学校的主键值</td>
	<td>学校的ID号</td>
</tr>
<tr>
	<td>account</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td>长度16</td>
	<td>账号</td>
</tr>
<tr>
	<td>password</td>
	<td>char</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td>必须包含字母、数字、可见字符，长度在12-16</td>
	<td>密码</td>
</tr>
<tr>
	<td>role</td>
	<td>tinyint</td>
	<td></td>
	<td>否</td>
	<td>0</td>
	<td></td>
	<td>角色</td>
</tr>
<tr>
	<td>value</td>
	<td>tinyint</td>
	<td></td>
	<td>否</td>
	<td>1</td>
	<td></td>
	<td>账号是否可用</td>
</tr>
</table>

#### 4. Teacher(教师)

<table cellspacing="0" id="teacher">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>可以为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值为自增</td>
	<td>主键值</td>
</tr>
<tr>
	<td>accountId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为账号表的主键值</td>
	<td>账号表的主键值</td>
</tr>
<tr>
	<td>teacherNo</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>教师编号</td>
</tr>
<tr>
	<td>name</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>名字</td>
</tr>
<tr>
	<td>gender</td>
	<td>char</td>
	<td></td>
	<td>是</td>
	<td></td>
	<td></td>
	<td>性别</td>
</tr>
<tr>
	<td>age</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>年龄</td>
</tr>
<tr>
	<td>position</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>职称</td>
</tr>
<tr>
	<td>degree</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>学历</td>
</tr>
<tr>
	<td>idCard</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>身份证号码</td>
</tr>

</table>


#### 5.Student(学生)
<table cellspacing="0" id="student">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>是否为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值为自增</td>
	<td>主键</td>
</tr>

<tr>
	<td>studentNo</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>学号</td>
</tr>
<tr>
	<td>accountId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为账号表的主键值</td>
	<td>账号表ID值</td>
</tr>
<tr>
	<td>name</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>名字</td>
</tr>
<tr>
	<td>gender</td>
	<td>char</td>
	<td></td>
	<td>是</td>
	<td></td>
	<td></td>
	<td>性别</td>
</tr>
<tr>
	<td>age</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>年龄</td>
</tr>
<tr>
	<td>academyId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为学院表的主键值</td>
	<td>学院ID值</td>
</tr>
<tr>
	<td>idcard</td>
	<td>varchar)</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td>格式为标准的身份证格式</td>
	<td>身份证号码</td>
</tr>
<tr>
	<td>major</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>专业</td>
</tr>
	<td>grade</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>年级</td>
</tr>
<tr>
	<td>classNo</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>班级号</td>
</tr>
<tr>
	<td>classId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为班的ID值</td>
	<td>班级编号</td>
</tr>
</table>

#### 6.Class(班级)
<table cellspacing="0" id="class">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>是否为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值为自增</td>
	<td>主键</td>
</tr>
<tr>
	<td>academyId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为学院的ID值</td>
	<td>学院的ID值</td>
</tr>
<tr>
	<td>grade</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>年级</td>
</tr>
<tr>
	<td>headTeacherNo</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>班主任编号</td>
</tr>
<tr>
	<td>size</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>班级总人数</td>
</tr>

</table>

#### 7.Course(课程)
<table cellspacing="0" id="course">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>是否为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值为自增</td>
	<td>主键</td>
</tr>
<tr>
	<td>name</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>课程名字</td>
</tr>
<tr>
	<td>academyId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为学院的ID值</td>
	<td>学院主键值</td>
</tr>
<tr>
	<td>teacherIds</td>
	<td>varchar</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为教师的ID值</td>
	<td>教师ID值的集合</td>
</tr>
<tr>
	<td>start</td>
	<td>datetime</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>开课时间</td>
</tr>
<tr>
	<td>grade</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>年级</td>
</tr>
<tr>
	<td>term</td>
	<td>int(1)</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>第几学期</td>
</tr>
<tr>
	<td>studentIds</td>
	<td>varchar</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为学生的ID值</td>
	<td>学生ID值集合</td>
</tr>
</table>

#### 8.Experiment(课程实验)
<table cellspacing="0" id="experiment">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>是否为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值为自增</td>
	<td>主键</td>
</tr>
<tr>
	<td>name</td>
	<td>varchar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>使用名称</td>
</tr>
<tr>
	<td>teacherId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为教师的主键值</td>
	<td>教师主键</td>
</tr>
<tr>
	<td>issueTime</td>
	<td>datetime</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>实验发布时间</td>
</tr>
<tr>
	<td>courseId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为课程表的主键值</td>
	<td>课程主键</td>
</tr>
</table>

#### 9.ExperimentScore(实验评分)
<table cellspacing="0" id="experimentScore">
<tr>
	<td>字段</td>
	<td>类型</td>
	<td>主键、外键</td>
	<td>是否为空</td>
	<td>默认值</td>
	<td>约束</td>
	<td>说明</td>
</tr>

<tr>
	<td>id</td>
	<td>int</td>
	<td>主键</td>
	<td>否</td>
	<td>1</td>
	<td>该值为自增</td>
	<td>主键</td>
</tr>
<tr>
	<td>score</td>
	<td>float</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>实验分数</td>
</tr>
<tr>
	<td>kind</td>
	<td>varhcar</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td>不同种类的汇报项目（PPT，代码...）</td>
	<td>分类</td>
</tr>
<tr>
	<td>occupy</td>
	<td>int</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>分数占比</td>
</tr>
<tr>
	<td>time</td>
	<td>datetime</td>
	<td></td>
	<td>否</td>
	<td></td>
	<td></td>
	<td>评分时间</td>
</tr>
<tr>
	<td>experimentId</td>
	<td>int</td>
	<td>外键</td>
	<td>否</td>
	<td></td>
	<td>取值范围为实验的主键值</td>
	<td>实验ID值</td>
</tr>
<tr>
	<td>review</td>
	<td>varchar</td>
	<td></td>
	<td>是</td>
	<td></td>
	<td></td>
	<td>评语</td>
</tr>
</table>

### 6.部分用例以及界面设计：

#### a. 登录用例：

a1.用例规约：<br>
<table cellspacing="0" style="width:900px;">
<tr>
	<td>用例名称</td>
	<td>登录</td>	
</tr>
<tr>
	<td>功能</td>
	<td>进入该系统以便进行后续的操作</td>	
</tr>
<tr>
	<td>参与者</td>
	<td>学生、教师</td>	
</tr>
<tr>
	<td>前置条件</td>
	<td>进入该系统的登录页面</td>	
</tr>
<tr>
	<td>后置条件</td>
	<td>登录成功，进入对应角色的主页</td>	
</tr>
<tr>
	<td>主流事件</td>
	<td>
	用户输入正确的账号、密码以及对应的角色,成功登陆进系统，<br>
	并将相应的用户信息保存在本地的Cookie中，<br>
	以便下次登录时不用重新输入账号信息
	</td>	
</tr>
<tr>
	<td>备选流事件</td>
	<td>
	 a.输入的用户名或者密码为空 :<br> 
     1.提示输入不能为空 <br>    
	 2.重新输入后需再次提交表单<br>
    b.输入的用户名或者密码错误:<br>
	1.修改用户名或者密码   <br>
	2.重新输入后需再次提交表单
    </td>
</tr>
	
</table>		

a2.业务流程图：<br>
![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My8.png)<br>
<br>
源码：<br>
@startuml<br>
actor 用户<br>
用户->登录页:验证用户信息<br>
alt 验证通过<br>
用户->实验管理系统:进入实验管理系统<br>
else 验证失败<br>
用户->登录页:重新输入用户信息<br>
end<br>
@enduml<br>
a3.界面设计：<br>
![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My3.png)<br>
a4.数据表：<br>
Account表

#### b. 个人信息修改用例：

b1.用例规约：<br>
<table cellspacing="0" style="width:900px;">
<tr>
	<td>用例名称</td>
	<td>个人信息修改</td>	
</tr>
<tr>
	<td>功能</td>
	<td>修改个人的一些相关信息</td>	
</tr>
<tr>
	<td>参与者</td>
	<td>学生、教师</td>	
</tr>
<tr>
	<td>前置条件</td>
	<td>登陆成功该系统</td>	
</tr>
<tr>
	<td>后置条件</td>
	<td></td>	
</tr>
<tr>
	<td>主流事件</td>
	<td>
	用户输入正确需要修改的信息后，点击提交后系统进行相应的数据修改，然后返回给用户修改后的信息。
	</td>	
</tr>
<tr>
	<td>备选流事件</td>
	<td>
		a.输入的修改信息不合法：<br> 
		 &nbsp;1.提示输入有效的数据 <br>    
		 &nbsp;2.重新输入后需再次提交表单<br><br>
		b.数据修改异常，服务器内部错误： <br> 
		 &nbsp;1.刷新页面后，重新填写修改信息 <br>    
		 &nbsp;2.重新输入后需再次提交表单<br><br>
	</td>	
</tr>
	
</table>	
b2.业务流程图：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My9.png)<br>
<br>
源码：<br>
@startuml<br>
actor 用户<br>
用户 -> 系统:成功登陆该系统<br>
用户->个人信息:个人信息查询<br>
系统-->用户:显示个人信息<br>
用户-> 系统:输入新的个人信息，进行修改<br>
系统-> 个人信息:修改个人信息<br>
系统 -->用户:提示修改成功与否<br>
@enduml<br>
b3.界面设计：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My4.png)<br>
b4.数据表：<br>
Account表/Teacher表/Student表

#### c. 密码修改用例：

c1.用例规约：<br>
<table cellspacing="0" style="width:900px;">
<tr>
	<td>用例名称</td>
	<td>密码修改</td>	
</tr>
<tr>
	<td>功能</td>
	<td>对个人的登录密码进行修改操作</td>	
</tr>
<tr>
	<td>参与者</td>
	<td>学生、教师</td>	
</tr>
<tr>
	<td>前置条件</td>
	<td>成功登陆该系统</td>	
</tr>
<tr>
	<td>主流事件</td>
	<td>
	用户输入正确的旧密码和修改的密码值，以及传入对应的账号值，<br>
	系统进行相应的数据库修改操作，操作完成后，提示密码修改成功后，重新回到登陆页面。
	</td>	
</tr>
<tr>
	<td>备选流事件</td>
	<td>
	a.输入的新密码为空： <br> 
	 &nbsp;1.提示密码不能为空 <br>    
	 &nbsp;2.重新输入后需再次提交表单<br><br>
	b.输入的密码不合法：<br>
	 &nbsp;1.修改输入的密码值，同时包含数字、字母、特殊符号 <br>    
	 &nbsp;2.重新输入后需再次提交表单
	</td>	
</tr>
	
</table>		

c2.业务流程图：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My10.png)<br>
<br>
源码：<br>
@startuml<br>
actor 用户<br>
用户->登陆页面:进入系统登录页面<br>
用户->系统:登陆成功<br>
用户->系统:密码修改<br>
系统->账号密码:进入密码修改页面<br>
alt 密码修改成功<br>
系统-->用户:提示密码修改成功<br>
系统-->登陆页面:重新登陆<br>
else 密码修改失败<br>
系统-->用户:提示修改失败<br>
系统-->账号密码:进入密码修改页面<br>
end<br>
@enduml<br>
c3.界面设计：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My5.png)<br>
c4.数据表：<br>
Account表/Teacher表/Student表

#### d. 学生信息列表用例：

d1.用例规约：<br>
<table cellspacing="0" style="width:900px;">
<tr>
	<td>用例名称</td>
	<td>学生信息列表查询</td>	
</tr>
<tr>
	<td>功能</td>
	<td>查询某一课程的学生信息列表</td>	
</tr>
<tr>
	<td>参与者</td>
	<td>教师</td>	
</tr>
<tr>
	<td>前置条件</td>
	<td>登陆成功进入该系统，且角色为教师</td>	
</tr>
<tr>
	<td>主流事件</td>
	<td>
	用户输入对应的课程值以及传入个人的编号值，后台系统根据传入的教师编号和课程的编号值查询出对应下的学生信息列表，返回给教师
	</td>	
</tr>
<tr>
	<td>备选流事件</td>
	<td>
	1.输入的课程不存在 <br> 
	 &nbsp;2.提示未教授该课程<br>    
	 &nbsp;3.重新输入后需再次提交表单<br>
	</td>	
</tr>
	
</table>		
d2.业务流程图：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My11.png)<br>
<br>
源码：<br>
@startuml<br>
actor 教师<br>
教师->系统 :成功登陆该系统<br>
教师->课程:查询教授的课程<br>
课程->学生信息列表:查询该课程下的所有学生信息列表<br>
学生信息列表 -->教师:以二维表的形式返回<br>
@enduml<br>
d3.界面设计：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My6.png)<br>
d4.数据表：<br>
Student表

#### e. 成绩查询用例：

e1.用例规约：<br>
<table cellspacing="0" style="width:900px;">
<tr>
	<td>用例名称</td>
	<td>查询成绩</td>	
</tr>
<tr>
	<td>功能</td>
	<td>查询学生最终成绩</td>	
</tr>
<tr>
	<td>参与者</td>
	<td>学生</td>	
</tr>
<tr>
	<td>前置条件</td>
	<td>成功登陆该系统</td>	
</tr>
<tr>
	<td>主流事件</td>
	<td>
	输入学生的ID号，系统查询数据库中的成绩返回给登入用户
	</td>	
</tr>
<tr>
	<td>备选流事件</td>
	<td>
	1.id输入错误，查询失败，提示错误id<br>
	2.请求超时，提示网络状况出错，稍后再试
	</td>	
</tr>
	
</table>		

e2.业务流程图：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My12.png)<br>
<br>
源码：<br>
@startuml<br>
actor 用户<br>

用户-->系统:成功登陆该系统<br>
alt 用户为老师<br>
用户-> 课程:查询某一教授课程<br>
课程 -> 学生信息列表:查询所授课程的学生信息列表<br>
学生信息列表->用户:以二维表的行返学生列表<br>
学生 ->实验:查询出已评定的实验<br>
实验分数-->用户:显示实验的分数<br>
else 用户为学生<br>
用户 -> 课程: 查询某一课程<br>
课程-> 实验:查询已评定的实验成绩<br>
实验 --> 用户:显示已评定的实验成绩<br>
实验分数-->用户:显示实验的分数<br>
end<br>
@enduml<br>
e3.界面设计：<br>

![Alt text](https://raw.githubusercontent.com/312922143/is_analysis/master/test6/My7.png)<br>
e4.数据表：<br>
Test表/TestSub表/TestScore表/TestSub_TestScore表
