---
layout: post
title: 虚拟环境配置(ubuntu & windows)和运行Jupyter Notebook
categories: 开发环境
description: 在ubuntu或windows下创建虚拟环境
keywords: 虚拟环境，ubuntu，Windows，开发环境，Jupyter Notebook
---


# ubuntu下创建虚拟环境
## 1. 虚拟环境

简单说：虚拟环境就是解决不同项目需要不同环境而产生的冲突问题。

## 2. 安装
```python
sudo pip install virtualenv    # 创建独立python环境的工具
sudo pip install virtualenvwrapper  # 基于virtualenv之上的工具，它将所有的虚拟环境统一管理
```
## 3. 配置
   **（1）创建虚拟环境管理目录**	
   ```python
   mkdir ~/.virtualenvs  
   ```
   **（2）设置环境变量**	
  ```python
  # 打开 .bashrc 文件
  sudo vim ~/.bashrc

 # 在.bashrc中添加如下内容
export WORKON_HOME=$HOME/.virtualenvs  # 所有虚拟环境存储的目录
 # export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
 # export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
source /usr/local/bin/virtualenvwrapper.sh   # virtualenvwrapper.sh所在路径

 # 启用配置文件
source ~/.bashrc
```

1. 注：以上配置是 ubuntu18.04
	 ```python
		# ubuntu16.04 的配置路径
		source /usr/local/bin/virtualenvwrapper.sh  
2. 启动配置文件 `source ~/.bashrc` 时，报错
	报错类型：
	```python
	# source ~/.bashrc  或 打开终端时 报错
	/usr/bin/python: No module named virtualenvwrapper
	virtualenvwrapper.sh: There was a problem running the initialization hooks.
	
	If Python could not import the module virtualenvwrapper.hook_loader,
	check that virtualenvwrapper has been installed for
	VIRTUALENVWRAPPER_PYTHON=/usr/bin/python and that PATH is
	set properly.
	
	 # 解决办法： sudo vim ~/.bashrc  将下面的两行注释打开 即可
	export WORKON_HOME=$HOME/.virtualenvs 
	# export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
	# export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
	source /usr/local/bin/virtualenvwrapper.sh	

	
	# 以上不行添加，在~/.bashrc文件的最下方加入下面语句
	 if [ -f /usr/local/bin/virtualenvwrapper.sh ]; then
	        export WORKON_HOME=$HOME/.virtualenvs
	        export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3  # 将ubuntu中路径设置为python3（当py2和py3共存的时候）
	        source /usr/local/bin/virtualenvwrapper.sh
	fi
	```	


## 4. 基本操作
**（1）创建虚拟环境**
```python
mkvirtualenv py_env  # py_env 是虚拟环境的名称
```
**（2）创建指定版本的虚拟环境**
```puthon
mkvirtualenv -p /usr/bin/python3.6  py3.6  # 根据python具体路径而定
```
**（3）使用虚拟环境**
```python
workon py3.6
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190429135815307.png)        
**（4）查看已创建的虚拟环境**
```python
workon + 回车   或   workon + 两次tab
```
**（5）退出虚拟环境**
```python
deactivate
```
**（6）删除虚拟环境**
```python
rmvirtualenv py3.6
```
**（7）批量安装第三方依赖包到虚拟环境**
```python
 pip install -r requirements.txt
 ```
 **（9）pycharm 安装包的导出**
 ```python
 pip freeze > requirements.txt
 ```
  **（10）查看虚拟环境安装包**
```python
pip freeze
```
# windows下创建虚拟环境
## 1. 安装
```python
sudo pip install virtualenv 
sudo pip install virtualenvwrapper-win
注：建议在 打开cmd时的默认路径下安装，不然后期使用时要切换到安装目录下使用
```
## 2. 配置(可省略，使用默认就好)
修改windows环境下mkvirtualenv.bat文件，配置虚拟环境根目录地址
> virtualenvwrapper安装完成后，打开Python根目录`\Scripts`目录下的`mkvirtualenv.bat`文件，如：` C:\Users\DELL\Envs\py37\Scripts\mkvirtualenv.bat,
`
> 注： `C:\Users\DELL\Envs` 其中 Envs文件就是虚拟环境管理文件，所有创建的虚拟环境都在此文件下。
## 3. 基本操作
>**注： ubuntu & windows 下创建虚拟环境方法和使用基本一致（基本操作同上）。**

#  在虚拟环境中运行Jupyter Notebook
- 切换到虚拟环境下
- 安装Jupyter Kernel：ipykernel
```python
pip install ipykernel
```
- 连接虚拟环境到Jupyter Kernel
```python
python -m ipykernel install --user --name 虚拟环境名称 --display-name "Jupyter中环境简称"
```


*注：书写此博客主要为了个人记忆方便及记录工作中的总结。
主要参考：
https://www.cnblogs.com/lxr1995/p/9140538.html
https://www.cnblogs.com/lliuye/p/10149932.html*
