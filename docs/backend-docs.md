
## 数据库设计

数据库会根据功能的设计发生变化，以下是最初版本数据库设计的ER图：  
![database](img/db.png "db")  

## 后端接口实现记录

### 学生中心首页

#### 用户登录（张慧斌）

```JavaScript

/api/student/log_in POST
Request
{
    "name": 1612941,// 此处的属性名参考数据库，代表“用户名”。
    "password_hash": awgyu223
}

Response
{
    "state_code":0,  // 0-成功，-1-用户名不存在，1-密码不正确
    "id": 139179
}
```

#### 用户查看个人信息（张慧斌）（哈斯普拉提）

```JavaScript

/api/student/personal_information GET
Request
{
    "id_user": 1612841
}

Response
{
 "name": "xrx",
 "student_number": 1612941,
"rank_score": 238,
"gender": 0,  // 新增性别
 "email": 1612941@mail.nankai.edu.cn
}

```

### 课程界面

#### 用户查看课程列表（张慧斌）（哈斯普拉提）

```JavaScript
/api/student/course GET
Request
{
    "id_user": 1612941
}

Response
[{
courses: [{
"name": "数据结构",
 "start_time": ”2019-4-1 14:00:00”,
"end_time": ”2019-4-2 14:00:00”,
 "description":"数据结构课",
"teacher": "刘明铭"  // 新增老师姓名
}]
}]
```

#### 用户提交实验报告（张慧斌，费德立）

```JavaScript
/api/student/lab_attachment_hand_in POST
Request
{
"id_user":123,
"id_course": 1234  // 新增课程的信息
"id_lab":123,
"file"//本地路径地址
}

{
state_code  // 0-成功，-1-上传失败
}
```

#### 用户下载资源（张慧斌，曹亮）

```JavaScript
/api/student/download_resource GET
Request
{
    "id_course_resource"： 123  // 课程资源id，在course_resourse表中查找
}

Response
[{
"name": "课件"
"path": "https://www.yuque.com/docs/share/e2db0e32-8463-4eac-b532-04bc6709eaa5"
}]

```

### 题目界面

#### 用户查看题目详情（魏家奇，张慧斌）

```JavaScript
/api/student/problem_detail GET
Request
{
"problem_id": id,  // 题目id
}

Response
{
      “name”:“Traveler",
      “start_time”:”2019-4-1 14:00:00”,
      “end_time”:”2019-4-1 15:00:00”,
      “description”:”旅行者问题”，  // 课程的具体描述
"cases": [{
"id": 1,
"input": 10,
"output": "No!",
"weight": 0.2  // 测试样例占比
}]
"runtime_limit": 1000ms,
"memory_limit": 64000KB
}
```

#### 用户提交题目（魏家奇，张慧斌）

```JavaScript
/api/student/problem_hand_in POST
Request
{
"user_id": 1,
"problem_id": 2,   // 从数据库来看，所有的提交记录都存在一张表problem_submission中
"code": "#include<iostream>\r\nint main(){cout<<123;\r\nreturn 0;}"
}

{
"runtime": 300ms,
"memory": 648KB
}
```

#### 用户查看某一道题目的提交记录（魏家奇，张慧斌，费德立）

```JavaScript
/api/student/problem_hand_in GET
Request
{
"user_id": 1,
"problem_id": 2
}
{
"created_at": 2019-4-1 14:00:00
"runtime": 300ms,
"memory": 648KB,
"score": 20/100，
"language": C++,
"code":"#include<iostream>\r\nint main(){cout<<123;\r\nreturn 0;}"
}
```