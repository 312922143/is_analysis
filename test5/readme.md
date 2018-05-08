# 实验5：图书管理系统数据库设计与界面设计

## 1.数据库表设计

## 1.1. Book表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|ISBN|varchar2(14)|主键|否| | | 为书本印刷的ISBN号|
|bookname|varchar2(60)| |否||||
|publisher|varchar2(100)| |是||||
|price|double| |否|0.0|||
|totalNum|int| |否|0| |库存|
|restNum|int| |否|0| |可借阅量|
|shortcontent|int| |是|0| |简介内容|
|publishingtime|datetime| |是|0| |出版时间|

## 1.2. Administrator表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|userID|varchar2(32)|主键|否||||
|username|varchar2(32)| |否| 'root'|||
|password|varchar2(32)| |否| '31292213'| ||
|gender|varchar2(32)| |是| '1'| |1为男，0为女|
|mail|varchar2(32)| |是| '31292213@qq.com'| ||
|adress|varchar2(32)| |是| | ||
|age|varchar2(32)| |是| '35'| ||
|telephone|varchar2(32)| |是| '18380277144'| ||

## 1.3. Reader表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|userID|varchar2(32)|主键|否||||
|username|varchar2(32)| |否| | ||
|password|varchar2(32)| |否| '123456789'| | |
|academy|varchar2(50)| |是| | |学院|
|age|varchar2(32)| |是| '21'| ||
|gender|varchar2(32)| |是| '1'| |1为男，0为女|
|mail|varchar2(32)| |是| '31292273@qq.com'| ||
|major|varchar2(32)| |是| '软件工程'| |就读专业|
|time|varchar2(32)| |是| '2018-5-9'| |最后登陆日期|

## 1.4. LendRecord表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|lendRecordRecordID|varchar2(32)|主键|否| | ||
|userID|varchar2(32)|外键|否| |Reader.userID||
|ISBN|varchar2(14)|外键|否| |Book.ISBN||
|startDate|datetime| |否| | |借阅时间|
|activeTime|int| |否|30| |一次借阅时间长度，单位为天|
|isRenew|tinyint| |否|0| 0-1|是否续借图书，1为已续借，0为未续借|
|returnDate|datetime| |是| | |归还时间，若为空代表没归还|
|bill|datetime| |是| | |违约时长，为空代表当前没有违期|

***

## 2. 界面设计
## 2.1. 图书查询界面设计
![pic1](pic.PNG)
- 用例图参见：图书查询用例
- 类图参见：Book类，Reader类，LendRecord类
- 顺序图参见：图书查询顺序图
- API接口如下：

1. 查询到的图书API

- 功能：用于获取某用户查询图书
- 请求地址： http://localhost/v1/api/get_books
- 请求方法：POST
- 请求参数：

|参数名称|必填|说明|
|:-------:|:-------------: | :----------:|
|userID|是|根据图书名获取图书列表 |

- 返回实例：
```
{
	"find": [{
		"ISBN": "9787513501231",
		"bookname": "岛",
		"publisher": "杨氏出版社",
		"rest": "3",
        "publishingtime":2015-11-22
	},
	{
    		"ISBN": "9787513501221",
    		"bookname": "穿越森林的男孩",
    		"publisher": "杨氏出版社",
    		"rest": "0",
            "publishingtime":2015-11-22
    	},
    	{
          		"ISBN": "9787513501231",
          		"bookname": "线",
          		"publisher": "杨氏出版社",
          		"rest": "4",
                  "publishingtime":2015-11-22
          	}],
	"status": "1"
}

```
- 返回参数说明：
    
|参数名称|说明|
|:-------:|:-------------: |
|find|用户查询图书集合|
|status|获取结果，为1时表示成功获取，为0时表示获取失败|
