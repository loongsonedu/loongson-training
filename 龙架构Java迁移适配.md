### 一、实验目的

* 了解实验平台虚拟机的使用
* 了解龙架构Java/SpringBoot应用迁移适配

### 二、实验准备
* 用户devuser密码：devuser
* 项目前后端及数据库地址：https://github.com/loongsonedu/springboot-api.git，包含项目前端coursefront、项目后端course的jar包、配置文件及数据库ry.sql
* 创建工作目录：mkdir workroom
* 进入工作目录：cd workroom
* 安装git命令：sudo apt install git
* 在工作目录克隆实验所需项目：git clone https://github.com/loongsonedu/spring-api.git
* 回到home目录：cd ~
### 三、系统验证
#### 1、MySQL安装及使用
##### mysql的安装及初始化
* 安装MySQL命令：sudo apt install default-mysql-server
* 查看MySQL是否安装成功：mysql -V
* 启动MySQL命令：sudo service mysql start
* 注：MySQL第一次启动可能会有个error报错，可以忽略此错误
* 输入：sudo mysql进入MySQL
* 输入：use mysql;
* update user set authentication_string=PASSWORD("devuser") where User='root';
* update user set plugin="mysql_native_password";
* flush privileges;
* quit;
* 重启MySQL服务：sudo service mysql restart
##### 数据库使用及导入.sql文件
* mysql -uroot -p 回车输入修改后的MySQL密码进入MySQL
* create database 数据库名（ry）; 回车
* use 数据库名（ry);进入数据库
* source workroom/spring-api/ry.sql(数据库.sql文件路径);
* 导入完成后执行：show tables; 查看数据库表
#### 2、jdk的安装及使用
* 安装jdk命令：sudo apt install openjdk-8-jdk
* 查看jdk版本命令：java -version
* 运行Java的jar包命令：找到jar包所在位置，输入sudo java -jar 要运行jar包的名字.jar
#### 3、redis的安装及配置
* 安装redis命令：sudo apt install redis
* 查看redis版本命令：redis-server -v
* 修改redis密码：找到/etc/redis/redis.conf文件，使用 sudo vim /etc/redis/redis.conf命令进入配置文件
* 如果出现提示，按 E 进入
* 输入：i 进入编辑模式，在最后加入requirepass devuser，即redis密码
* 按 esc 键退出编辑模式，按 Shift+：输入wq 保存并退出
* 启动redis命令： sudo service redis-server start
#### 4、前端所需环境安装
* 安装node命令：sudo apt install nodejs
* 安装npm命令：sudo apt install npm
* 安装yarn命令：需要先更改npm仓库 npm config set registry https://registry.npm.taobao.org/
* 查看npm仓库：npm config get registry
* 安装yarn：sudo npm install -g yarn
* 修改npm源：npm config set registry https://registry.loongnix.cn:4873
### 四、项目运行
##### 前端项目运行：
* 输入 ：cd workroom/springboot-api/coursefront进入coursefront目录
* 输入node版本兼容命令：yarn config set ignore-engines true
* 输入：yarn install 加载依赖
* 输入：yarn dev 运行前端项目
##### 后端项目运行：
* 再打开一个终端
* 进入/course/jar/config/中，找到两个.yml配置文件，将其中的redis、MySQL数据库名字、密码改为自己设置的
将MySQL、redis等中间件启动完成后启动/course/jar中的.jar文件（默认密码为devuser，MySQL、redis密码根据操作步骤设置为devuser则不用更改密码）
* 输入 ：cd workroom/spring-api/course/jar进入jar包目录
* 启动后端项目命令：sudo java -jar ruoyi-admin.jar
* 前端已经设置好.env文件与后端接口VITE_API_BASE_URL=http://localhost:8080
* 后端运行成功后 ，将http://localhost:5173/course/网址右键复制，黏贴至龙芯浏览器进入即可显示实验最终结果
* api验证：
* 1、http://localhost:8080/seller/api/coursesget/getAllCoursesByConditionsWithTotal?page=0&size=18&clientId=466&tag=hot&isDelete=1&sort=courseIndex,asc
* 2、http://localhost:8080/seller/api/teachers/getAllTeachersByConditionsWithTotal?page=0&size=6&clientId=466
* 3、http://localhost:8080/seller/api/homepages?clientId=466
* 4、http://localhost:8080/seller/api/students?clientId=466&courseId=104&size=2000
* 5、http://localhost:8080/seller/api/course-classes?clientId=466&courseId=104&size=2000&sort=startAt,desc
