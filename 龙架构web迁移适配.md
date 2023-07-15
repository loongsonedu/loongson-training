### 一、实验目的

* 了解实验平台虚拟机的使用
* 了解龙架构web应用迁移适配

### 二、实验准备
1. 用户devuser 密码：devuser

    后续执行sudo需要输入的密码devuser

2. 网络设置

    1. 
        ```
        sudo vi /etc/apt/sources.list 
        ```
        把文件内容中的 **http** 修改为 **https**。（tips：shift + zz 可以保存退出）
        [如图](https://github.com/loongsonedu/loongson-training/assets/920487/1ffdaab7-6fcb-4ebc-9162-428700cd2a29)

    2. 修改完成后，**重新刷新页面**，注意这一步很重要

    3. 
        ```
        sudo apt-get update
        ```
3. 安装 nodejs   

    ```
    sudo apt install nodejs
    ```
    结束后可执行 ```node -v``` 查看安装情况, 输出版本信息说明安装成功

4. 安装 npm   

    ```
    sudo apt install npm
    ```
    结束后可执行 ```npm -v``` 查看安装情况, 输出版本信息说明安装成功

5. 安装 yarn   

    ```
    sudo npm install -g yarn --registry=https://registry.npm.taobao.org
    ```
    结束后可执行 ```yarn -v``` 查看安装情况, 输出版本信息说明安装成功

6. 创建并进入到工作目录中

    ```
    mkdir frontroom && cd frontroom
    ```

### 三、开始迁移项目

1. 把 **course** 项目克隆至本地

    1. 
        ```
        git clone -b feat/loongson https://ghproxy.com/https://github.com/loongsonedu/course.git
        ```
        执行该条命令后，git会把course仓库的**feat/loongson**分支克隆至本地

    2. 然后进入到项目中 
        ```
        cd course
        ```
2. 修改 **npm** 配置，忽略对node版本的限制

    ```
    yarn config set ignore-engines true
    ```

 3. 安装项目依赖

    ```
    yarn install
    ```
 4. 创建环境变量

    1. 通过env.exmaple复制出.env文件(注意.env文件前面加点)
        ```
        cp env.example .env
        ```
    2. 修改.env文件中的**VITE_API_BASE_URL**变量
        ```
        vi .env
        ```

        ```
        VITE_API_BASE_URL=https://admin.maodouketang.com:8443
        ```
        该环境变量的作用是让项目知道从哪台服务器获取数据

5. 运行项目

    ```
    yarn run dev
    ```

    启动成功后， 打开浏览器访问 http://localhost:5173/course/

6. 打包并预览项目

    ```
    yarn run build && yarn run preview
    ```

    启动成功后， 打开浏览器访问 http://localhost:4173/course/

7. 修改配置文件sit.config.js    

    修改该文件中的logo、title等字段来更新页面的基础信息

    如果使用了yarn run preview运行项目, 则需要重新打包


### 四、QA过程中可能会遇到的问题

1. 无法安装node、npm等基础软件，链接不上软件包

    参考"二、 实验准备" 部分第2条，修改/etc/apt/sources.list文件，把文件内容中的http改为https

    修改为完成后重新刷新页面，然后执行```sudo apt-get update```后在尝试安装需要软件

2. yarn run dev 运行报错

    运行项目如遇到下图错误，说明esbuild版本有问题

    <img width="400" alt="WeChatWorkScreenshot_9151b0d5-4ccb-45e1-95e1-f1bb8de89b79" src="https://github.com/loongsonedu/loongson-training/assets/920487/9296af42-6764-4efe-afc1-1e3a8edcab17">

    我们需要安装正确的esbuild版本

    ```
    $ yarn add -D esbuild --registry=https://registry.loongnix.cn:4873
    $ rm -rf node_modules/vite/node_modules
    ```

    执行完以上两条命令后再重新运行项目

3.  yarn run dev 无法启动

    如果出错原因不是上一条, 则不通过yarn run dev 运行项目

    直接打包构建输出

    ```
        yarn run build && yarn run preview
    ```

4. yarn run dev 正常运行后，通过浏览器访问页面, 一直显示数据加载中，无有效内容展示。

    可能是环境变量没配置好

    1. 需要检查是否创建了 **.env** 文件

    2. **.env** 文件中配置的 **VITE_API_BASE_URL**是否设置正确

    ```
    VITE_API_BASE_URL=https://admin.maodouketang.com:8443
    ```