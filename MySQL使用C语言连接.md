<a name="thTSR"></a>
# MySQL使用C语言连接
<a name="CkM0p"></a>
## 引入库
要使用C语言连接MySQL，需要使用MySQL官网提供的库。

<a name="BJqaH"></a>
### 下载库文件
> 下载库文件

首先，进入[MySQL官网](https://www.mysql.com/)，选择DEVELOPER [ZONE](https://so.csdn.net/so/search?q=ZONE&spm=1001.2101.3001.7020)（开发人员专区），然后点击MySQL Downloads。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689504646516-ed426745-041f-44b8-bc91-7b6c3f35aa6c.png#averageHue=%23fbfaf9&clientId=u9bbf220a-0da5-4&from=paste&height=789&id=uc85af9dc&originHeight=986&originWidth=1894&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=319108&status=done&style=none&taskId=ubb9340f2-952b-4ce3-bd62-dbd879c8752&title=&width=1515.2)


接下来选择Download Archives。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689504534306-949e7fb0-d9fe-49ae-a357-95c54c427429.png#averageHue=%23fdfcfc&clientId=u9bbf220a-0da5-4&from=paste&height=791&id=uf62e0628&originHeight=989&originWidth=1854&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=129204&status=done&style=none&taskId=ucd5b048c-23e6-4b12-bda3-75ce9dac73f&title=&width=1483.2)


因为我们是要使用C语言连接MySQL，所以这里选择MySQL Connector/C。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689504749036-f27ee5e6-0296-4654-b9e7-0042bb4d8c3e.png#averageHue=%23fdfcfc&clientId=u9bbf220a-0da5-4&from=paste&height=712&id=u174d7486&originHeight=890&originWidth=1851&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=117420&status=done&style=none&taskId=u83a06a13-0c1b-4d68-8b29-20be01abdc1&title=&width=1480.8)


最后选择适合自己平台的mysql connect库，然后点击下载就行了。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689504813247-ccaeb48b-b96b-4ea0-a1a2-d37f4bb0bd44.png#averageHue=%23faf9f4&clientId=u9bbf220a-0da5-4&from=paste&height=425&id=u840ff2a3&originHeight=531&originWidth=1835&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=74313&status=done&style=none&taskId=u0f06c793-73d6-443e-ad58-80b05ea88de&title=&width=1468)


> 上传到云服务器

因为我下载的是Linux下使用的库文件，因此下载完毕后需要将其上传到云服务器，我准备将下载的库文件存放在一个名为thirdPath的目录下。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689505025329-0e33133d-acfb-4690-996b-651eef09ab06.png#averageHue=%230c0a08&clientId=u9bbf220a-0da5-4&from=paste&height=145&id=u1abd881e&originHeight=181&originWidth=597&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=16216&status=done&style=none&taskId=ub91ed089-d2df-4c5f-a05d-75a2e8818ca&title=&width=477.6)<br /> 

使用rz -E命令将刚才下载的库文件上传到云服务器。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689506291624-4a33d918-cca6-438a-9097-6064f229a51f.png#averageHue=%23191817&clientId=u9bbf220a-0da5-4&from=paste&height=615&id=u0d47d49a&originHeight=769&originWidth=1888&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=117371&status=done&style=none&taskId=ue72efd68-14cc-4693-a9c5-ab1a650ee3c&title=&width=1510.4)

然后使用tar命令将压缩包解压到当前目录下。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689506627569-d80d71aa-51d3-45d3-bf3e-ee478d3526f5.png#averageHue=%230e0806&clientId=u9bbf220a-0da5-4&from=paste&height=68&id=u789e3b7c&originHeight=85&originWidth=1032&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=14863&status=done&style=none&taskId=uc969f8e2-d3f2-4b9f-9aea-5faa63783f4&title=&width=825.6)

为了方便后面演示，这里使用mv命令将解压后的目录名称改短一点。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689506769131-d988d719-a711-4b71-b81b-0b08a5e50ce2.png#averageHue=%230e0806&clientId=u9bbf220a-0da5-4&from=paste&height=93&id=u9de36bc8&originHeight=116&originWidth=1089&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=21605&status=done&style=none&taskId=u5af0711b-4514-44ff-a43d-18dff306b56&title=&width=871.2)


进入解压后的目录当中，可以看到有一个include子目录和一个lib子目录。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689506878707-8dcfebc3-6599-406e-a2ec-a767b8e2788b.png#averageHue=%23090604&clientId=u9bbf220a-0da5-4&from=paste&height=146&id=u95ac0989&originHeight=182&originWidth=734&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=19409&status=done&style=none&taskId=u1329d2c2-c8bc-4184-b5d9-e3f63298c42&title=&width=587.2)

其中，include目录下存放的一堆头文件。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689506911926-12fc2dbc-02b0-4ca9-a14f-cc892133a482.png#averageHue=%23080503&clientId=u9bbf220a-0da5-4&from=paste&height=130&id=u4a19cd58&originHeight=162&originWidth=1728&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=25042&status=done&style=none&taskId=uff1da1e7-f5b3-4618-88d2-09b1c41d2e4&title=&width=1382.4)

而lib目录下存放的就是动静态库。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689506957119-8e377e1b-0fe3-4c83-ba20-e282849fab38.png#averageHue=%23070503&clientId=u9bbf220a-0da5-4&from=paste&height=67&id=u029a8fa6&originHeight=84&originWidth=873&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=11800&status=done&style=none&taskId=u6302a83a-a1f6-4de5-9ed6-5738035c92c&title=&width=698.4)

<a name="yGlcq"></a>
### 在项目中使用库
> 在项目中使用库

为了方便在项目中使用刚才的库文件，可以在项目目录下创建两个软连接，分别连接到刚才的include目录和lib目录。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689508012978-af2d34dc-a5a4-4217-9a8c-9b8147833b06.png#averageHue=%23160a07&clientId=u9bbf220a-0da5-4&from=paste&height=110&id=u28316d37&originHeight=138&originWidth=1052&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=23369&status=done&style=none&taskId=u8e8aa4f6-b25c-4cb4-9bd7-e30c7093c16&title=&width=841.6)

这时直接在项目目录下，就能看到刚才include和lib目录下的内容。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689508096992-6794dbe9-dd73-4aa7-871e-45821a911627.png#averageHue=%230d0907&clientId=u9bbf220a-0da5-4&from=paste&height=50&id=uc0c67caf&originHeight=63&originWidth=885&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=7113&status=done&style=none&taskId=ue56d93f3-0295-4131-b514-ad53d7e56ff&title=&width=708)

下面先通过调用mysql_get_client_info来判断库是否引入成功，该函数的作用就是获取客户端的版本信息。<br />代码如下：
```cpp
#include <iostream>
#include <mysql.h>
using namespace std;

int main()
{
    //获取客户端的版本信息
    cout<<"mysql client version: "<<mysql_get_client_info()<<endl;

    return 0;
} 
```


为了方便后续重复编译源文件，可以在项目目录下创建一个Makefile，Makefile当中的内容如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689508499520-55f774e0-0e93-4b17-bd1e-96ca3a06cdf5.png#averageHue=%231d1d1c&clientId=u9bbf220a-0da5-4&from=paste&height=159&id=u150a9ba8&originHeight=199&originWidth=1110&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=17634&status=done&style=none&taskId=u9b0552a5-899e-45dd-a635-69c2bd8f874&title=&width=888)<br />**说明一下：**

- -I：用于指明头文件的搜索路径。
- -L：用于指明库文件的搜索路径。
- -l：用于指明需要连接库文件路径下的哪一个库。


Makefile编写完毕后，直接通过make命令即可编译代码生成可执行程序。但此时生成的可执行程序还不能直接运行，通过ldd命令可以看到，该可执行程序所依赖的mysqlclient库找不到。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689508749104-728a6d0a-a46d-4f21-893a-14698ee75a7c.png#averageHue=%23130e0d&clientId=u9bbf220a-0da5-4&from=paste&height=245&id=u3edc6e57&originHeight=306&originWidth=1883&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=58267&status=done&style=none&taskId=u63f7d9ea-4dd2-42b5-a795-e14e8f33254&title=&width=1506.4)


**原因如下：**

- gcc/g++编译器默认都是动态链接的，编译代码时默认使用的是动态库，所以生成的可执行程序在运行时需要找到对应的动态库进行链接，而我们使用的mysqlclient库并不在系统的搜索路径下。
- 需要注意的是，Makefile中的-I，-L和-l这三个选项，只是在编译期间告诉编译器头文件和库文件在哪里，而可执行程序生成后就与编译器无关了。


**解决该问题通常有三种做法：**

1. 将库文件拷贝到系统默认的库文件搜索路径下/lib64。
2. 将库文件所在的目录路径添加到LD_LIBRARY_PATH环境变量中，该环境变量可以用于指定查找动态库时的其他路径。
3. 将库文件所在的目录路径保存到以.conf为后缀的配置文件中，然后将该文件拷贝到/etc/ld.so.conf.d/目录下，并使用ldconfig命令对配置文件进行更新，该目录下所有配置文件中的路径也将作为查找动态库时的搜索路径。

这里我们采用第三种方式进行解决。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509065500-55ea20c3-f88a-4397-8705-b573c37cfc72.png#averageHue=%230f0a09&clientId=u9bbf220a-0da5-4&from=paste&height=190&id=u61cbd5ee&originHeight=237&originWidth=1585&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=43330&status=done&style=none&taskId=u10c4389b-5043-4f02-b89f-a523e67273c&title=&width=1268)

此时该可执行程序所依赖的mysqlclient库就能够被找到了。如下![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509138491-1f9b056b-cc14-4fb3-a0aa-f53d9db0c8a3.png#averageHue=%23140d0c&clientId=u9bbf220a-0da5-4&from=paste&height=265&id=u8c131a49&originHeight=331&originWidth=1658&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=59710&status=done&style=none&taskId=u0d0d5614-018e-41e2-988f-505ae08f9a2&title=&width=1326.4)

运行可执行程序后，可以看到客户端的版本为6.1.11，也就是刚才下载的库文件的版本。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509193685-715af115-6ea8-42c1-8ee0-bc4bd5c6d15d.png#averageHue=%23060303&clientId=u9bbf220a-0da5-4&from=paste&height=150&id=u2f2e6cb7&originHeight=187&originWidth=1197&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=17169&status=done&style=none&taskId=u59cc1593-91bb-4f42-977d-efcf8ab6c27&title=&width=957.6)

<a name="kmD5N"></a>
## 使用库
至此库已经成功被引入，剩下就是库接口的使用问题了。
<a name="nQeb8"></a>
### 连接数据库
> 创建MySQL对象

在连接数据库之前，需要先创建一个MySQL对象，创建MySQL对象的函数如下：<br />` MYSQL* mysql_init(MYSQL *mysql); `

**说明一下**

- 该函数用来分配或者初始化一个MySQL对象，用于连接MySQL服务器。
- 如果传入的参数是NULL，那么mysql_init将自动为你分配一个MySQL对象并返回。
- 如果传入的参数是一个地址，那么mysql_init将在该地址处帮你完成初始化。

MYSQL对象中包含了各种信息，其类型定义如下：
```cpp
typedef struct st_mysql {
	NET net;			/* Communication parameters */
    unsigned char	*connector_fd;		/* ConnectorFd for SSL */
    char *host,*user,*passwd,*unix_socket,*server_version,*host_info;
    char *info, *db;
    struct charset_info_st *charset;
    MYSQL_FIELD	*fields;
    MEM_ROOT field_alloc;
    my_ulonglong affected_rows;
    my_ulonglong insert_id;		/* id if insert on table with NEXTNR */
    my_ulonglong extra_info;		/* Not used */
    unsigned long thread_id;		/* Id for connection in server */
    unsigned long packet_length;
    unsigned int port;
    unsigned long client_flag,server_capabilities;
    unsigned int protocol_version;
    unsigned int field_count;
    unsigned int server_status;
    unsigned int server_language;
    unsigned int warning_count;
    struct st_mysql_options options;
    enum mysql_status status;
    my_bool	free_me;		/* If free in mysql_close */
    my_bool	reconnect;		/* set to 1 if automatic reconnect */

    /* session-wide random string */
    char scramble[SCRAMBLE_LENGTH+1];
    my_bool unused1;
    void *unused2, *unused3, *unused4, *unused5;

    LIST *stmts;                     /* list of all statements */
    const struct st_mysql_methods *methods;
    void *thd;
    /*
      Points to boolean flag in MYSQL_RES  or MYSQL_STMT. We set this flag
      from mysql_stmt_close if close had to cancel result set of this object.
    */
    my_bool *unbuffered_fetch_owner;
    /* needed for embedded server - no net buffer to store the 'info' */
    char *info_buffer;
    void *extension;
} MYSQL;

```

**说明一下：**

- MYSQL对象中的methods变量是一个结构体变量，该变量里面保存着很多函数指针，这些函数指针将会在数据库连接成功以后的各种数据操作中被调用。

> 连接数据库

创建完MySQL对象后就可以连接数据库了，连接数据库的函数如下：
```cpp
MYSQL* mysql_real_connect(MYSQL *mysql, const char *host,
					const char *user,
					const char *passwd,
					const char *db,
					unsigned int port,
					const char *unix_socket,
					unsigned long clientflag); 
```

**参数说明：**

- mysql： 表示在连接数据库前，调用mysql_init函数创建的MySQL对象。
- host： 表示需要连接的MySQL服务器的IP地址，"127.0.0.1"表示连接本地MySQL服务器。
- user： 表示连接MySQL服务器时，所使用用户的用户名。
- passwd： 表示连接MySQL服务器时，所使用用户的密码
- db： 表示连接MySQL服务器后，需要使用的数据库。
- port： 表示连接的MySQL服务器，所对应的端口号。
- unix_socket： 表示连接时应该使用的套接字或命名管道，通常设置为NULL。
- clientflag： 可以设置为多个标志位的组合，表示允许特定的功能，通常设置为0。

**返回值说明：**

- 如果连接数据库成功，则返回一个MySQL对象，该对象与第一个参数的值相同。
- 如果连接数据库失败，则返回NULL。

> 关闭数据库连接

与数据库交互完毕后，需要关闭数据库连接，关闭数据库连接的函数如下：<br />`void mysql_close(MYSQL *sock); `

**说明一下：**

- 该函数的参数，就是连接数据库前调用mysql_init创建的MySQL对象。
- 如果传入的MySQL对象是mysql_init自动创建的，那么调用mysql_close时就会释放这个对象。

> 连接示例

比如使用如下代码连接我的MySQL服务器：
```cpp
#include <iostream>
#include <string>
#include <mysql.h>
using namespace std;

const string host = "49.232.66.206";
const string user = "dragon";
const string passwd = "3524nwe@ytkrSJTEW";
const string db = "connect_demon";
const int port = 3306;

int main()
{
    //1、创建MySQL对象
    MYSQL* ms = mysql_init(nullptr);
    //2、连接数据库
    if(mysql_real_connect(ms, host.c_str(), user.c_str(), passwd.c_str(), db.c_str(), port, nullptr, 0) == nullptr)
    {
        cerr<<"数据库连接失败!"<<endl;
        return 1;
    }
    cout<<"数据库连接成功!"<<endl;

    //3、关闭数据库
    mysql_close(ms);
    cout<<"数据库关闭成功!"<<endl;
    return 0;
} 
```


使用make命令生成可执行程序，运行后即可看到连接数据库成功、关闭数据库成功。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509454724-f5873ed6-55a6-4a51-8480-901e0a3b9269.png#averageHue=%230c0807&clientId=u9bbf220a-0da5-4&from=paste&height=157&id=ub224d3e4&originHeight=196&originWidth=1300&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=28634&status=done&style=none&taskId=u41932793-72cb-432f-80f5-e81f3eb6671&title=&width=1040)


<a name="NDi2N"></a>
### 下发SQL请求
> 下发SQL请求

与数据库建立连接期间，就可以向MySQL服务器下发SQL请求，下发SQL请求的函数如下：<br />`in mysql_query(MYSQL *mysql, const char *q);`      

**参数说明：**

- **mysql：** 表示在连接数据库前，调用mysql_init函数创建的MySQL对象。
- **q：** 表示向MySQL服务器下发的SQL请求，SQL最后可以不带分号。

**返回值说明：**

- 返回值为0表示SQL执行成功，否则表示SQL执行失败。

> 设置编码格式

在连接数据库之后，需要统一客户端和服务器的编码格式，避免在数据交互过程中出现乱码，设置编码格式的函数如下：<br />`int mysql_set_character_set(MYSQL *mysql, const char *csname);`

**参数说明：**

- **mysql：** 表示在连接数据库前，调用mysql_init函数创建的MySQL对象。
- **csname：** 表示要设置的编码格式，如"utf8"。

**返回值说明：**

- 返回值为0表示设置成功，否则表示设置失败。

> 测试表介绍

下面在与MySQL数据库交互时，访问的都是connect_demon数据库，该数据库下有一个user表，表中有三条记录。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509614201-de864010-ce83-411f-8528-dafb08ed532b.png#averageHue=%23080504&clientId=u9bbf220a-0da5-4&from=paste&height=497&id=u44fab3cc&originHeight=621&originWidth=1184&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=44677&status=done&style=none&taskId=ud0f31287-e576-4f49-83c8-aa9908cf38f&title=&width=947.2)


> 向数据库中插入数据

在调用mysql_query函数时，向MySQL服务器下发一条insert SQL。如下：
```cpp
#include <iostream>
#include <string>
#include <mysql.h>
using namespace std;

const string host = "49.232.66.206";
const string user = "dragon";
const string passwd = "3524nwe@ytkrSJTEW";
const string db = "connect_demon";
const int port = 3306;

int main()
{
    //1、创建MySQL对象
    MYSQL* ms = mysql_init(nullptr);
    //2、连接数据库
    if(mysql_real_connect(ms, host.c_str(), user.c_str(), passwd.c_str(), db.c_str(), port, nullptr, 0) == nullptr)
    {
        cerr<<"数据库连接失败!"<<endl;
        return 1;
    }
    cout<<"数据库连接成功!"<<endl;
    mysql_set_character_set(ms, "utf8"); //设置编码格式为utf8
    
    //3、向数据库表中插入记录
    std:string sql = "insert into user values (4,'赵六',25)";
    if(mysql_query(ms, sql.c_str()) != 0)
    {
        cout<<"插入数据失败!"<<endl;
        return 2;
    }
    cout<<"插入数据成功!"<<endl;

    //4、关闭数据库
    mysql_close(ms);
    cout<<"数据库关闭成功!"<<endl;
    return 0;
}

```


使用make命令生成可执行程序，运行后在MySQL中即可看到对应数据被成功插入。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509735983-c1dbfbd7-92cc-44e1-8289-b30fe8cbce5d.png#averageHue=%23110f0f&clientId=u9bbf220a-0da5-4&from=paste&height=538&id=ubb10b9fe&originHeight=673&originWidth=1889&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=84566&status=done&style=none&taskId=u4e1f0702-0f5a-4dcc-9bb7-93f93180648&title=&width=1511.2)


> 删除数据库中的数据

在调用mysql_query函数时，向MySQL服务器下发一条delete SQL。如下：
```cpp
#include <iostream>
#include <string>
#include <mysql.h>
using namespace std;

const string host = "49.232.66.206";
const string user = "dragon";
const string passwd = "3524nwe@ytkrSJTEW";
const string db = "connect_demon";
const int port = 3306;

int main()
{
    //1、创建MySQL对象
    MYSQL* ms = mysql_init(nullptr);
    //2、连接数据库
    if(mysql_real_connect(ms, host.c_str(), user.c_str(), passwd.c_str(), db.c_str(), port, nullptr, 0) == nullptr)
    {
        cerr<<"数据库连接失败!"<<endl;
        return 1;
    }
    cout<<"数据库连接成功!"<<endl;
    mysql_set_character_set(ms, "utf8"); //设置编码格式为utf8
    
    //3、删除数据库表中的记录
    std:string sql = "delete from user where id=4";
    if(mysql_query(ms, sql.c_str()) != 0)
    {
        cout<<"删除数据失败!"<<endl;
        return 2;
    }
    cout<<"删除数据成功!"<<endl;

    //4、关闭数据库
    mysql_close(ms);
    cout<<"数据库关闭成功!"<<endl;
    return 0;
}

```

使用make命令生成可执行程序，运行后在MySQL中即可看到对应数据被成功删除。如下：![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509813819-d6fbb0ad-6c67-4e27-b1fc-5a73a092071a.png#averageHue=%23161514&clientId=u9bbf220a-0da5-4&from=paste&height=398&id=uc59e2d0d&originHeight=497&originWidth=1885&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=70354&status=done&style=none&taskId=u6869365f-4e8d-4206-b44e-f176784c60f&title=&width=1508)



> 修改数据库中的数据

在调用mysql_query函数时，向MySQL服务器下发一条update SQL。如下：
```cpp
#include <iostream>
#include <string>
#include <mysql.h>
using namespace std;

const string host = "49.232.66.206";
const string user = "dragon";
const string passwd = "3524nwe@ytkrSJTEW";
const string db = "connect_demon";
const int port = 3306;

int main()
{
    //1、创建MySQL对象
    MYSQL* ms = mysql_init(nullptr);
    //2、连接数据库
    if(mysql_real_connect(ms, host.c_str(), user.c_str(), passwd.c_str(), db.c_str(), port, nullptr, 0) == nullptr)
    {
        cerr<<"数据库连接失败!"<<endl;
        return 1;
    }
    cout<<"数据库连接成功!"<<endl;
    mysql_set_character_set(ms, "utf8"); //设置编码格式为utf8
    
    //3、修改数据库表中的记录
    std:string sql = "update user set age=22 where id=1";
    if(mysql_query(ms, sql.c_str()) != 0)
    {
        cout<<"修改数据失败!"<<endl;
        return 2;
    }
    cout<<"修改数据成功!"<<endl;

    //4、关闭数据库
    mysql_close(ms);
    cout<<"数据库关闭成功!"<<endl;
    return 0;
} 
```

使用make命令生成可执行程序，运行后在MySQL中即可看到对应数据被成功修改。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689509960806-cdf8b5e6-c4af-427d-b2b5-00e1e1fdce36.png#averageHue=%23100f0f&clientId=u9bbf220a-0da5-4&from=paste&height=536&id=ueefec4c0&originHeight=670&originWidth=1889&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=78926&status=done&style=none&taskId=u705d5d17-8f32-42d3-b11c-40e98c34eb6&title=&width=1511.2)


<a name="m1GJh"></a>
### 获取查询结果
> 获取查询结果

- 对数据库中的数据进行增删改操作时，都只需要调用mysql_query向服务器下发对应的SQL请求。
- 而对数据库中的数据进行查询操作时，除了需要调用mysql_query向服务器下发对应的查询SQL，还需要获取查询结果。

获取查询结果的函数如下：<br />`MYSQL_RES* mysql_store_result(MYSQL *mysql);`

**说明一下：**

- 该函数会调用指定MySQL对象中对应的函数指针来获取查询结果，并将获取到的查询结果保存到MYSQL_RES变量中进行返回。
- 需要注意的是，MYSQL_RES变量的内存空间是malloc出来的，因此在使用完后需要调用free函数进行释放，否则会造成内存泄露。

MYSQL_RES变量中保存了查询得到的各种信息，其类型定义如下：
```cpp
typedef struct st_mysql_res {
	my_ulonglong  row_count;
	MYSQL_FIELD	*fields;
	MYSQL_DATA	*data;
	MYSQL_ROWS	*data_cursor;
	unsigned long *lengths;		/* column lengths of current row */
	MYSQL		*handle;		/* for unbuffered reads */
    const struct st_mysql_methods *methods;
    MYSQL_ROW	row;			/* If unbuffered read */
    MYSQL_ROW	current_row;		/* buffer to current row */
    MEM_ROOT	field_alloc;
    unsigned int	field_count, current_field;
    my_bool	eof;			/* Used by mysql_fetch_row */
    /* mysql_stmt_close() had to cancel this result */
    my_bool       unbuffered_fetch_cancelled;
    void *extension;
} MYSQL_RES;

```



> 获取查询结果的行数

获取查询结果的行数的函数如下：<br />`my_ulonglong mysql_num_rows(MYSQL_RES *res);`<br />**说明一下：**

- 该函数将会从指定的MYSQL_RES对象中，获取查询结果的行数。



> 获取查询结果的列数

获取查询结果的列数的函数如下：<br />`unsigned int mysql_num_fields(MYSQL_RES *res);`<br />**说明一下：**

- 该函数将会从指定的MYSQL_RES对象中，获取查询结果的列数。

> 获取查询结果的列属性

获取查询结果的列属性的函数如下：<br />`MYSQL_FIELD* mysql_fetch_fields(MYSQL_RES *res);`<br />**说明一下：**

- 该函数将会从指定的MYSQL_RES对象中，获取查询结果的列属性。



mysql_fetch_fields函数将会返回多个MYSQL_FIELD对象，每个MYSQL_FIELD对象中保存着对应列的各种列属性，其类型定义如下：
```cpp
typedef struct st_mysql_field {
	char *name;                 /* Name of column */
	char *org_name;             /* Original column name, if an alias */
	char *table;                /* Table of column if column was a field */
	char *org_table;            /* Org table name, if table was an alias */
	char *db;                   /* Database for table */
	char *catalog;	      /* Catalog for table */
	char *def;                  /* Default value (set by mysql_list_fields) */
	unsigned long length;       /* Width of column (create length) */
	unsigned long max_length;   /* Max width for selected set */
	unsigned int name_length;
	unsigned int org_name_length;
	unsigned int table_length;
	unsigned int org_table_length;
	unsigned int db_length;
	unsigned int catalog_length;
	unsigned int def_length;
	unsigned int flags;         /* Div flags */
	unsigned int decimals;      /* Number of decimals in field */
	unsigned int charsetnr;     /* Character set */
	enum enum_field_types type; /* Type of field. See mysql_com.h for types */
	void *extension;
} MYSQL_FIELD;

```



> 获取查询结果中的一行数据

获取查询结果中的一行数据的函数如下：<br />`MYSQL_ROW mysql_fetch_row(MYSQL_RES *result);`<br />**说明一下：**

- 该函数将会从指定的MYSQL_RES对象中，获取查询结果中的一行数据。

MYSQL_ROW对象中保存着一行数据，这一行数据中可能包含多个字符串，对应就是这行数据中的多个列信息，因此MYSQL_ROW本质就是char**类型，其类型定义如下：<br />`typedef char **MYSQL_ROW;       /* return data as array of strings */`



> 查询示例

比如查询user表中的数据并进行打印输出。如下：
```cpp
#include <iostream>
#include <string>
#include <mysql.h>
using namespace std;

const string host = "49.232.66.206";
const string user = "dragon";
const string passwd = "3524nwe@ytkrSJTEW";
const string db = "connect_demon";
const int port = 3306;

int main()
{
    //1、获取MySQL实例（相当于给我们创建了一个MySQL句柄）
    MYSQL* ms = mysql_init(nullptr);
    //2、连接数据库
    if(mysql_real_connect(ms, host.c_str(), user.c_str(), passwd.c_str(), db.c_str(), port, nullptr, 0) == nullptr)
    {
        cerr<<"数据库连接失败!"<<endl;
        return 1;
    }
    cout<<"数据库连接成功!"<<endl;
    mysql_set_character_set(ms, "utf8"); //设置编码格式为utf8
    
    //3、查询数据库表中的记录
    //a、执行查询语句
    std:string sql = "select * from user";
    if(mysql_query(ms, sql.c_str()) != 0)
    {
        cout<<"查询数据失败!"<<endl;
        return 2;
    }
    cout<<"查询数据成功!"<<endl;
    //b、获取查询结果
    MYSQL_RES* res = mysql_store_result(ms);
    int rows = mysql_num_rows(res); //数据的行数
    int cols = mysql_num_fields(res); //数据的列数
    //获取每列的属性并打印列名
    MYSQL_FIELD* fields = mysql_fetch_fields(res);
    for(int i = 0;i < cols;i++)
    {
        cout<<fields[i].name<<"\t";
    }
    cout<<endl;
    for(int i = 0;i < rows;i++)
    {
        //获取一行数据并进行打印
        MYSQL_ROW row = mysql_fetch_row(res);
        for(int j = 0;j < cols;j++)
        {
            cout<<row[j]<<"\t";
        }
        cout<<endl;
    }
    free(res); //释放内存空间
    
    //4、关闭数据库
    mysql_close(ms);
    cout<<"数据库关闭成功!"<<endl;
    return 0;
}

```


使用make命令生成可执行程序，运行后在即可看到数据的查询结果。如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/29339358/1689510288938-5742b427-eca7-42b0-bd99-45626552425c.png#averageHue=%23080605&clientId=u9bbf220a-0da5-4&from=paste&height=242&id=ufd2dfb8e&originHeight=303&originWidth=1285&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=41178&status=done&style=none&taskId=ue3e9251c-80e8-421f-b82d-c9b264704cb&title=&width=1028)
