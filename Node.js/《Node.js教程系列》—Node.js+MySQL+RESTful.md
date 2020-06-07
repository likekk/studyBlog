> 点赞再看、养成习惯。



> 寄语：长风破浪会有时，直挂云帆济沧海。
> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile: :smile: ,共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将GitHub上规划前端学习的路线和资源分享。



### 前言

最近学习了一下Node.js相关的内容，在这里初步做个小总结，说实话关于本篇博客的相关内容，自己很久之前就已经有过学习，但是你懂的，**“好记性不如烂笔筒”**，学过的东西不做笔记的话，很容易就会忘记的一干二净，往往的结果就是自己又要重头开始学习，这是一个非常痛苦的过程。没有办法，为了重新捡起自己曾经学过的内容，决定写下这篇博客来回顾自己所学的知识



### 本章目标

#### Node.js后端

- 学会使用node.js操作MySQL实现简单的增删查改
- 学会使用RESTful风格定义接口

#### web前端

- 学会使用vue2整合Ajax
- 学会使用vue2整合axios



### 项目搭建

#### MySQL数据库

**数据库脚本**

创建鲜花信息表，添加鲜花编号，鲜花名称，鲜花价格，鲜花用途，鲜花花材，鲜花花语等字段。在这里我们就直接使用SQL脚本来创建数据表和添加一些测试数据。

```sql
CREATE table flowerinfo
(
    fid BIGINT auto_increment PRIMARY key not NULL COMMENT"编号",
    fname varchar(20) not null COMMENT"名称",
    fprice DECIMAL(16,2)  COMMENT"价格",
    fsituation varchar(20) not null COMMENT"使用节日",
    fuse varchar(20) not null COMMENT"鲜花用途",
    fhc varchar(20) not null COMMENT"鲜花花材",
    fword varchar(50) COMMENT"花语"
)COMMENT"鲜花信息表"

INSERT into flowerinfo(fname,fprice,fhc,fuse,fsituation,fword)
VALUES("一生一世",200,"玫瑰,香槟","爱情鲜花","情人节","你是我一生一世唯一的爱人,我会好好珍惜你"),
("祝福你",300,"玫瑰,香槟","爱情鲜花","情人节,母亲节,父亲节","我把我最真诚的祝福送给你,祝你天天开心"),
("一生一世",200,"玫瑰,香槟","爱情鲜花","情人节","你是我一生一世唯一的爱人,我会好好珍惜你"),
("祝福你",300,"玫瑰,香槟","爱情鲜花","情人节,母亲节,父亲节","我把我最真诚的祝福送给你,祝你天天开心")
```

**结果：**

![](https://img2018.cnblogs.com/i-beta/1475945/201911/1475945-20191121220456127-294380820.png)



#### Node.js后端项目搭建

##### 1、搭建node.js项目

搭建node.js项目的过程我就直接省略了，具体如何搭建node.js项目大家可以自行百度或者后期我会添加相关内容的博客方便大家学习。搭建好的项目结构如下：

![](https://img2018.cnblogs.com/i-beta/1475945/201911/1475945-20191121221415398-2107607748.png)

##### 2、安装mysql依赖

既然我们需要操作mysql，那么我们肯定需要安装相关的依赖，在这里介绍三种方法安装mysql依赖。



**方式一：**

```javascript
npm install cnpm --registry=https://registry.npm.taobao.org 
cnpm install mysql　　//使用淘宝镜像依赖mysql
```



**方式二：**

```javascript
npm install mysql --save    //　当前项目安装mysql依赖
```



**方式三：**

```javascript
npm install mysql -g　　　　//全局安装mysql依赖
```



选择任意以上一种方法安装都可以，安装完成之后，我们确认一下是否真的安装成功，找到目录node_modules,这里是查看我们安装的所有依赖，可以看到mysql依赖成功了。

![](https://img2018.cnblogs.com/i-beta/1475945/201911/1475945-20191121221842158-296753206.png)



##### 3、编写RESTful风格的接口

找到目录结构routes，新建flowerRouter.js文件。目录结构如下：

![](https://img2018.cnblogs.com/i-beta/1475945/202001/1475945-20200128163248486-1346081703.png)



一、建立node.js和mysql数据库的连接

```javascript
let express=require('express'); //  引入express依赖
let mysql=require('mysql')  //  引入mysql依赖
let router=express.Router();
let connection=mysql.createConnection({
    host: 'localhost',   //主机名
    user:'root',    //账号
    password:'123456',    //密码
    database:'flower'   //连接的数据库名称
});
connection.connect();   //建立连接
```

|        参数        |                             描述                             |
| :----------------: | :----------------------------------------------------------: |
|        host        |                 主机地址 （默认：localhost）                 |
|        user        |                            用户名                            |
|      password      |                             密码                             |
|        port        |                    端口号 （默认：3306）                     |
|      database      |                          数据库名称                          |
|      charset       | 连接字符集（默认：'UTF8_GENERAL_CI'，注意字符集的字母都要大写） |
|    localAddress    |                   此IP用于TCP连接（可选）                    |
|     socketPath     |       连接到unix域路径，当使用 host 和 port 时会被忽略       |
|      timezone      |                    时区（默认：'local'）                     |
|   connectTimeout   |             连接超时（默认：不限制；单位：毫秒）             |
|  stringifyObjects  |                        是否序列化对象                        |
|      typeCast      |     是否将列值转化为本地JavaScript类型值 （默认：true）      |
|    queryFormat     |                  自定义query语句格式化方法                   |
| supportBigNumbers  | 数据库支持bigint或decimal类型列时，需要设此option为true （默认：false） |
|  bigNumberStrings  | supportBigNumbers和bigNumberStrings启用 强制bigint或decimal列以JavaScript字符串类型返回（默认：false） |
|    dateStrings     | 强制timestamp,datetime,data类型以字符串类型返回，而不是JavaScript Date类型（默认：false） |
|       debug        |                   开启调试（默认：false）                    |
| multipleStatements |       是否许一个query中有多个MySQL语句 （默认：false）       |
|       flags        |                       用于修改连接标志                       |
|        ssl         | 使用ssl参数（与crypto.createCredenitals参数格式一至）或一个包含ssl配置文件名称的字符串，目前只捆绑Amazon RDS的配置文件 |

具体参数信息请前往：[mysql配置信息](https://github.com/mysqljs/mysql)

二、完整代码：

```javascript
let express=require('express'); //  引入express依赖
let mysql=require('mysql')  //  引入mysql依赖
let router=express.Router();
let connection=mysql.createConnection({
    host: 'localhost',   //主机名
    user:'root',    //账号
    password:'123456',    //密码
    database:'flower'   //连接的数据库名称
});
connection.connect();   //建立连接
//  查询全部鲜花信息
router.get('/getAllFlower',(req,res,next)=>{
    connection.query('select * from flowerinfo',(err,result)=>{
        if(err){
            throw  err;
            return;
        }
        res.send(result);
    })
});
//  添加鲜花信息
router.post('/addFlower',(req,res,next)=>{
    let fname=req.body.fname;  //名称
    let fprice=req.body.fprice;//  价格
    let fsituation=req.body.fsituation;    //节日
    let fuse=req.body.fuse;    //  用途
    let fhc=req.body.fhc;      //  花材
    let fword=req.body.fword;  //花语
    let addsql="insert into flowerinfo(fid,fname,fprice,fsituation,fuse,fhc,fword)values(0,?,?,?,?,?,?)";
    let addsqlParams=[fname,fprice,fsituation,fuse,fhc,fword];
    connection.query(addsql,addsqlParams,(err,result)=>{
        if(err){
            throw err;
            return;
        }
        res.send('添加成功!');
    })
})
//  根据鲜花编号查询鲜花信息
router.get('/findFlowerById',(req,res,next)=>{
    let id=req.query.id;
    let selectsql='select * from flowerinfo where fid=?';
    let selctParams=[id];
    connection.query(selectsql,selctParams,(err,result)=>{
        if (err){
            throw  err
        }
        res.send(result);
    })
})
//  修改鲜花信息
router.put('/updateFlower',(req,res,next)=>{
    let id=req.body.fid;
    let fname=req.body.fname;  //名称
    let fprice=req.body.fprice;//  价格
    let fsituation=req.body.fsituation;    //节日
    let fuse=req.body.fuse;    //  用途
    let fhc=req.body.fhc;      //  花材
    let fword=req.body.fword;   //花语
    let updatesql='update flowerinfo set fname=?,fprice=?,fsituation=?,fuse=?,fhc=?,fword=? where fid=?';
    let updatesqlParams=[fname,fprice,fsituation,fuse,fhc,fword,id]
    connection.query(updatesql,updatesqlParams,(err,result)=>{
        if (err){
            throw  err;
            return false
        }
        res.send('修改成功!');
    })
})
//  删除鲜花信息
router.delete('/deleteFlower',(req,res,next)=>{
    let id=req.body.id;
    let deletesql="delete from flowerinfo where fid=?";
    let deletesqlParams=[id];
    connection.query(deletesql,deletesqlParams,(err,result)=>{
        if(err){
            throw  err;
            return false;
        }
        res.send('删除成功!');
    })
})
module.exports=router;
```



这里有个重大的bug，就是我们连接完之后没有关闭连接，这样就会资源的浪费，占用cpu。这里大家可以想办法去解决，由于我们这里是测试的，所以没有设置关闭连接。

**注意：**

> 结尾一定要写module.exports=router



##### 4、注册router和设置跨域请求

找到目录结构下的app.js文件注册路由和跨域请求设置。

![](https://img2018.cnblogs.com/i-beta/1475945/202001/1475945-20200128162808486-1563490211.png)



 **app.js文件代码**

```javascript
var createError = require('http-errors');
var express = require('express');
var path = require('path');
var cookieParser = require('cookie-parser');
var logger = require('morgan');

var indexRouter = require('./routes/index');
var usersRouter = require('./routes/users');
var productRouter=require('./routes/product');
var flowerRouter=require('./routes/flowerRouter')
var app = express();

// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');

app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));
//  设置跨域请求
app.all('*', function(req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "content-type");
    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS");
    res.header("X-Powered-By", ' 3.2.1');
    res.header("Content-Type", "application/json;charset=utf-8");
    if(req.method == "OPTIONS") {
        res.send("200");
    } else {
        next();
    }
});
app.use('/', indexRouter);
app.use('/users', usersRouter);
app.use('/product',productRouter);
app.use('/flower',flowerRouter);


// catch 404 and forward to error handler
app.use(function(req, res, next) {
  next(createError(404));
});

// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render('error');
});

module.exports = app;
```



**跨域代码：**

```javascript
//  设置跨域请求
app.all('*', function(req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "content-type");
    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS");
    res.header("X-Powered-By", ' 3.2.1');
    res.header("Content-Type", "application/json;charset=utf-8");
    if(req.method == "OPTIONS") {
        res.send("200");
    } else {
        next();
    }
});
```



#### web前端

前端方面主要使用两种方法操作数据，一种是ajax，另一种是axios，将所需要用到的插件引入。目录结构如下：

![](https://img2018.cnblogs.com/i-beta/1475945/202001/1475945-20200128163634332-1376421700.png)



 在这里我们引入的vue.js，axios，jQuey，以及新建两个html文件，为了方便命名上已经规定了。接下来就是数据操作了。

### vue2整合ajax

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax和vue操作mysql</title>
</head>
<body>
<div id="app">
    <table border="1" width="800px" style="margin: 0 auto" cellspacing="0" cellpadding="0">
        <tr>
            <td>编号</td>
            <td>名称</td>
            <td>价格</td>
            <td>使用节日</td>
            <td>鲜花用途</td>
            <td>鲜花花材</td>
            <td>花语</td>
            <td>操作</td>
        </tr>
            <template v-for="(item,index) of flowerArray">
                <tr>
                    <td>{{index+1}}</td>
                    <td>{{item.fname}}</td>
                    <td>{{item.fprice}}</td>
                    <td>{{item.fsituation}}</td>
                    <td>{{item.fuse}}</td>
                    <td>{{item.fhc}}</td>
                    <td>{{item.fword}}</td>
                    <td>
                        <input type="button" :data-id="item.fid" value="删除" @click="deleteFlower(item.fid)">
                        <input type="button" :data-id="item.fid" value="修改" @click="findFlowerById(item.fid)">
                    </td>
                </tr>
            </template>
    </table>
    <form>
        名称：
        <input type="text" v-model="fname"><br>
        价格：
        <input type="text" v-model="fprice"><br>
        节日：
        <input type="text" v-model="fsituation"><br>
        用途：
        <input type="text" v-model="fuse"><br>
        花材：
        <input type="text" v-model="fhc"><br>
        花语：
        <input type="text" v-model="fword"><br>
        <span style="color: red">{{result}}</span><br>
        <input type="button" @click="addFlower" value="添加鲜花">
        <input type="button" @click="updateFlower" value="修改鲜花">
    </form>
</div>
<script src="javascripts/jquery-3.3.1.min.js"></script>
<script src="javascripts/vue.js"></script>
<script>
    var vm=new Vue({
        el:'#app',
        data:{
            fid:'',
            fname:'',
            fprice:'',
            fsituation:'',
            fuse:'',
            fhc:'',
            fword:'',
            result:'',
            flowerArray:[],
        },
        mounted(){
            this.findAllFlower();
        },
        methods:{
          findFlowerById:function (id) {    //根据编号查询鲜花信息
              this.fid=id;
              $.ajax({
                  url:'http://localhost:3000/flower/findFlowerById',
                  type:'GET',
                  data:{id:id}
              }).done((data)=>{
                  this.fname=data[0].fname;
                  this.fprice=data[0].fprice;
                  this.fsituation=data[0].fsituation;
                  this.fuse=data[0].fuse;
                  this.fhc=data[0].fhc;
                  this.fword=data[0].fword;
              })
          },
            deleteFlower:function (id) {    //删除鲜花信息
                $.ajax({
                    url:'http://localhost:3000/flower/deleteFlower',
                    type:"DELETE",
                    data:{
                        id:id
                    },
                }).done((data)=>{

                })
            },
            addFlower:function () {         //  添加鲜花信息
                $.ajax({
                    url:'http://localhost:3000/flower/addFlower',
                    type:'POST',
                    data:{
                        fname:this.fname,
                        fprice:this.fprice,
                        fsituation:this.fsituation,
                        fuse:this.fuse,
                        fhc:this.fhc,
                        fword:this.fword,
                    }
                }).done((data)=>{
                })
            },
            updateFlower:function (id) {      //  修改鲜花信息
                $.ajax({
                    url:'http://localhost:3000/flower/updateFlower',
                    type:'PUT',
                    data:{
                        fid:this.fid,
                        fname:this.fname,
                        fprice:this.fprice,
                        fsituation:this.fsituation,
                        fuse:this.fuse,
                        fhc:this.fhc,
                        fword:this.fword,
                    },
                }).done((data)=>{

                })
            },
            findAllFlower:function () { //  查询全部鲜花信息
                $.ajax({
                    url:'http://localhost:3000/flower/getAllFlower',
                    type:"GET",
                    dataType:"json"
                }).done((data)=>{
                    this.flowerArray=data;
                })
            }
        },
    })

</script>
</body>
</html>
```



### vue2整合axios

为了更加方便的实现功能和理解，在这里我分步骤为大家讲解。争取有一个好的效果。vue整合axios其实和vue整合ajax差不多，如果想学习axios的相关文章，可以参考我的这一篇博客[axios参考笔记](https://www.cnblogs.com/jjgw/p/12079892.html)，这里面涉及关于axios的使用大部分讲解的都非常详细。欢迎大家评论和提出问题。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>axios和vue操作mysql</title>
</head>
<body>
<div id="app">
    <table border="1" width="800px" style="margin: 0 auto" cellspacing="0" cellpadding="0">
        <tr>
            <td>编号</td>
            <td>名称</td>
            <td>价格</td>
            <td>使用节日</td>
            <td>鲜花用途</td>
            <td>鲜花花材</td>
            <td>花语</td>
            <td>操作</td>
        </tr>
        <template v-for="(item,index) of flowerArray">
            <tr>
                <td>{{index+1}}</td>
                <td>{{item.fname}}</td>
                <td>{{item.fprice}}</td>
                <td>{{item.fsituation}}</td>
                <td>{{item.fuse}}</td>
                <td>{{item.fhc}}</td>
                <td>{{item.fword}}</td>
                <td>
                    <input type="button" :data-id="item.fid" value="删除" @click="deleteFlower(item.fid)">
                    <input type="button" :data-id="item.fid" value="修改" @click="findFlowerById(item.fid)">
                </td>
            </tr>
        </template>
    </table>
    <form>
        名称：
        <input type="text" v-model="fname"><br>
        价格：
        <input type="text" v-model="fprice"><br>
        节日：
        <input type="text" v-model="fsituation"><br>
        用途：
        <input type="text" v-model="fuse"><br>
        花材：
        <input type="text" v-model="fhc"><br>
        花语：
        <input type="text" v-model="fword"><br>
        <span style="color: red">{{result}}</span><br>
        <input type="button" @click="addFlower" value="添加鲜花">
        <input type="button" @click="updateFlower" value="修改鲜花">
    </form>
</div>
<script src="javascripts/vue.js"></script>
<script src="javascripts/axios.js"></script>
<script>
    var vm=new Vue({
        el:'#app',
        data:{
            fid:'',
            fname:'',
            fprice:'',
            fsituation:'',
            fuse:'',
            fhc:'',
            fword:'',
            result:'',
            flowerArray:[],
        },
        mounted(){
            this.findAllFlower();
        },
        methods:{
            findFlowerById:function (id) {    //根据编号查询鲜花信息
                this.fid=id;
                axios({
                    url:'http://localhost:3000/flower/findFlowerById',
                    type:'GET',
                    params:{id:id}
                }).then((data)=>{
                    console.log(data.data[0].fname);
                    this.fname=data.data[0].fname;
                    this.fprice=data.data[0].fprice;
                    this.fsituation=data.data[0].fsituation;
                    this.fuse=data.data[0].fuse;
                    this.fhc=data.data[0].fhc;
                    this.fword=data.data[0].fword;
                })
            },
            deleteFlower:function (id) {    //删除鲜花信息
                axios({
                    url:'http://localhost:3000/flower/deleteFlower',
                    method:"DELETE",
                    data:{
                        id:id
                    },
                }).then((data)=>{
                    this.result=data.data;
                })
            },
            addFlower:function () {         //  添加鲜花信息
                axios({
                    url:'http://localhost:3000/flower/addFlower',
                    method:'POST',
                    data:{
                        fname:this.fname,
                        fprice:this.fprice,
                        fsituation:this.fsituation,
                        fuse:this.fuse,
                        fhc:this.fhc,
                        fword:this.fword,
                    }
                }).then((data)=>{
                    this.result=data.data;
                })
            },
            updateFlower:function (id) {      //  修改鲜花信息
                axios({
                    url:'http://localhost:3000/flower/updateFlower',
                    method:'PUT',
                    data:{
                        fid:this.fid,
                        fname:this.fname,
                        fprice:this.fprice,
                        fsituation:this.fsituation,
                        fuse:this.fuse,
                        fhc:this.fhc,
                        fword:this.fword,
                    },
                }).then((data)=>{
                    this.result=data.data;
                })
            },
            findAllFlower:function () { //  查询全部鲜花信息
                axios({
                    url:'http://localhost:3000/flower/getAllFlower',
                    method:"GET",
                    dataType:"json"
                }).then((data)=>{
                    this.flowerArray=data.data;
                })
            }
        },
    })

</script>
</body>
</html>
```



### 结尾

如果觉得本篇文章对您有用的话，可以麻烦您给笔者点亮那个点赞按钮。
<img src="https://s1.ax1x.com/2020/03/23/8oGjfA.th.jpg">

对于杨戬这个暖男来说：**真的真的非常有用**，您的支持将是我继续写文章前进的动力，我们下篇文章见。

**【原创】|二郎神杨戬**

> 原创不易，莫要白嫖。
> 二郎神杨戬，一个在互联网前端苟且偷生的划水程序员，专注于前端开发，善于技术分享。
> 如需转载，请联系作者或者保留原文链接，微信公众号搜索二郎神杨戬或者扫描下方的二维码更加方便。
>
> 一起来见证二郎神杨戬的成长吧！更多好文、技术分享尽在下方这个公众号。欢迎关注。

<img src="https://s1.ax1x.com/2020/05/04/Y9LspR.png" />