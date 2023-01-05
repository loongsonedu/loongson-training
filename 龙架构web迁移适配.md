### 一、实验目的

* 了解实验平台虚拟机的使用
* 了解React框架
* 了解龙架构web应用迁移适配

### 二、实验准备
* 用户devuser密码：devuser
* course端git地址址：https://github.com/loongsonedu/course.git
* 安装git命令：sudo apt install git
* 实验项目在feat/node-14.16.1分支下
* 创建工作目录：mkdir frontroom
* 进入工作目录：cd frontroom
* 在工作目录克隆实验所需项目：git clone -b feat/loongson https://github.com/loongsonedu/course.git
* 回到home目录：cd ~
### 三、系统验证
#### web迁移适配所需环境安装
* 安装node命令：sudo apt install nodejs
* 安装npm命令：sudo apt install npm
* 安装yarn命令：需要先更改npm仓库 npm config set registry https://registry.npm.taobao.org/
* 查看npm仓库：npm config get registry
* 安装yarn：sudo npm install -g yarn
* 修改npm源：npm config set registry https://registry.loongnix.cn:4873
### 四、项目运行
#### 前端项目运行：
* 输入 ：cd frontroom/course进入course目录
* 输入node版本兼容命令：yarn config set ignore-engines true
* 根据README写接口文件
* 在前端项目中创建一个.env文件，输入 VITE_API_BASE_URL=http://114.242.206.180:25777
* 在 frontroom/course目录下创建.env文件：mkfile .env
* 输入：vim .env 命令创建并进入文件
* 若出现提示，按 E 进入
* 输入：i 进入编辑模式，输入入 VITE_API_BASE_URL=http://114.242.206.180:25777，即后端接口
* 按 esc 键退出编辑模式，按 Shift+：输入wq 保存并退出
* 输入：yarn install 加载依赖
* 输入：yarn dev 运行前端项目
* 运行成功显示网址：http://localhost:5173/course/
* 将http://localhost:5173/course/网址右键复制，黏贴至龙芯浏览器进入即可显示实验最终结果