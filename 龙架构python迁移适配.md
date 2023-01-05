### 实验目的 
* 通过学习龙芯下python编程，及其库的兼容性
* 了解python 办公库在龙芯下的工作原理
* 了解 兼容驱动lbrowserdriver的使用

### 环境安装
1. 
```
sudo apt-get install aptitude
```

输入密码: devuser,

输入Y

2.  
```
sudo aptitude install python3-pip
```
安装 pip3命令

3. 
```
pip3 install ipython
```

4. 增加path
```
vim .bashrc
```
增加
```
export PATH=$PATH:/home/devuser/.local/bin
```
保存退出后
执行
```
source .bashrc 
```



### 实验过程
安装excel 需要的库
```
1. pip3 install xlrd
2. pip3 install xlwt
3. pip3 install xlutils
```

安装 2007 excel 读写库
```
pip3 install openpyxl
```

安装爬虫库
```
pip3 install requests
```

安装 网页解析库
```
pip3 install bs4
```
安装依赖
```
sudo aptitude install libxml2 libxslt1.1 libxslt1-dev python-libxslt1 libzip-dev
pip3 install lxml
```
### 安装 driver包
```
sudo dpkg -i lbrowserdriver_3.2.1815.1-1.stable.loongarch64.deb 
```

安装selenium
pip3 install selenium

#### 使用样例:
```

In [1]: from selenium import webdriver

In [2]: br = webdriver.Chrome('lbrowserdriver')

In [3]: br.get("https://www.loongson.cn")

```


