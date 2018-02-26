
#windows

1、下载安装python（区分操作系统32/64 ）
https://www.python.org/downloads/release/python-351/

2、进入cmd(windows命令提示符)下面输入"python"命令。

（如果提示python不是内部或外部命令！配置环境变量）

修改我的电脑->属性->高级->环境变量->系统变量中的PATH为:

变量名：PATH

变量值：;C:\Python35;C:\Python35\Scripts; 

3、安装selenium

3.1、通过pip 安装 --

安装：
 #apt-get install python-pip

升级：
 #pip install -U pip

C:\Users\fnngj>python3 -m pip install selenium 

3.2、通过下载包安装

https://pypi.python.org/pypi/selenium

解压，cmd进入目录:

C:\selenium\selenium2.53.5> python3 setup.py install



#ubuntu
1、安装：setuptools

root@fnngj-H24X:~# apt-get install python -setuptools

2、安装pip

root@fnngj-H24X:/home/fnngj/python# tar -zxvf pip-1.4.1.tar.gz

root@fnngj-H24X:/home/fnngj/python# cd pip-1.4.1/ 

root@fnngj-H24X:/home/fnngj/python# python setup.py install

3、安装selenium

root@fnngj-H24X:/home/fnngj/python/pip-1.4.1# pip install -U selenium



#Chrome/IE
1、下载chrome driver，放到chrome的安装目录下
http://chromedriver.storage.googleapis.com/index.html

python3.4.4只支持firefox46以下的版本