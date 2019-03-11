# Jupyter Notebook无法连接到Kernel 如何重新安装



##Jupyter Notebook可以打开但无法使用

####现象

在 Terminal 中 jupyter notebook，打开的网页显示：

Python 3 右边显示断开的🔗，左边黄底字框 “Connecting to kernel”

Terminal中持续返回下图内容

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311Miniconda3/Screen%20Shot%202019-03-11%20at%203.57.20%20PM.png)

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311Miniconda3/Screen%20Shot%202019-03-11%20at%205.02.42%20PM.png)

Jupyter Notebook中的任何cell都无法运行，持续显示In[*]



####分析

经多方资料搜索，认为是以下两个问题：

1. mac系统下多版本共存，需要为 jupyter 指定python版本
2. Jupyter Notebook安装不正确

故需要重新安装 jupyter notebook



##指定系统的Python版本

####版本信息

macOS Mojave Version 10.14

Python 2.7（Mac自带的Python版本）

Python 3.7.1（2019.3从Python官网下载）

pip 19.0.3

Python官网：[Python](https://www.python.org)

https://www.python.org/downloads/



####升级pip版本

```
pip3 install –upgrade pip 
```

升级后查看pip版本，python2.7和python 3.7中的pip都被更新到了最新版本



####指定系统Python版本

使用官网下载的pkg安装好python 3.7.1，安装至默认目录

```
/Library/Frameworks/Python.framework/Versions/3.7
```

用此命令修改文件

```
vi ~/.bash_profile
```

添加PATH

```
# Setting PATH for Python 3.7
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.7/bin:${PATH}"
export PATH
alias python="/Library/Frameworks/Python.framework/Versions/3.7/bin/python3.7"
```



修改后bash_profile文件如下：

```
export GOROOT=/usr/local/go
export GOPATH=$(go env GOPATH)
export GOBIN=$GOPATH/bin
export GOARCH=amd64
export GOOS=darwin
export PATH=$PATH:$(go env GOPATH)/bin

# Setting PATH for Python 3.7
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.7/bin:${PATH}"
export PATH
alias python="/Library/Frameworks/Python.framework/Versions/3.7/bin/python3.7"

# If want to use Python 2.7, just comment # the alias line
# If want to use Python 3.7, just set the last line of alias free
# REMEMBER to restart the terminal after you comment or set free the alias line
# Once you've restart and type python --version in the terminal, you'll see the change of default version of Python in your system
```



reference: https://blog.csdn.net/luolianxi/article/details/81698391



## 不可控factor

在清理掉package之前，曾做过以下操作，产生对应变化。

不知是否为关键（不可跳过）步骤。

若单独清理package无效，请采取以下步骤



####kernel地址变化

```
python -m ipykernel install --user
```

查看kernel

```
jupyter kernelspec list 
```

kernel产生变化，kernel地址变化如下

```
Available kernels:
python3    /Library/Frameworks/Python.framework/Versions/3.7/share/jupyter/kernels/python3
```

```
Available kernels:
  python3    /Users/wangyu/Library/Jupyter/kernels/python3
```

**但此时在Terminal中 jupyter notebook 仍旧无法连接到Kernel 并使用 Run Cell**



reference: https://github.com/ipython/ipython/issues/10346



##清空原版本 Jupyter 及相关依赖

####清理Dependency

使用pip3 show jupyter找到 pip3 真正的package存放地址：

```
/Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages
```

返回全部内容如下

```
wangyudeMacBook-Pro:~ wangyu$ pip3 show jupyter
Name: jupyter
Version: 1.0.0
Summary: Jupyter metapackage. Install all the Jupyter components in one go.
Home-page: http://jupyter.org
Author: Jupyter Development Team
Author-email: jupyter@googlegroups.org
License: BSD
Location: /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages
Requires: qtconsole, jupyter-console, notebook, ipykernel, nbconvert, ipywidgets
Required-by:
```

在其中清理掉所有jupyter相关的package

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311Miniconda3/Screen%20Shot%202019-03-11%20at%208.36.14%20PM.png)



我清理掉了如下图所示的所有jupyter的dependencies

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311Miniconda3/Screen%20Shot%202019-03-11%20at%208.43.07%20PM.png)



####清理Package

也清理掉了这个目录

```
/Library/Frameworks/Python.framework/Versions/3.7/bin
```

里面 jupyter 的所有相关package

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311Miniconda3/Screen%20Shot%202019-03-11%20at%209.52.32%20PM.png)



## 重新安装 Jupyter

用pip3重新安装jupyter notebook

```
pip3 install jupyter
```



至此，全部package已安装至（真正 package 安装地址）

```
/Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages
```



全部dependency也已安装至（pip3 list所得到的返回表）

```
/Library/Frameworks/Python.framework/Versions/3.7/bin
```





##检验 Jupyter Notebook 可否正常运行

然后重新输入命令打开jupyter notebook

```
jupyter notebook
```



返回值如下：

```
wangyudeMacBook-Pro:~ wangyu$ jupyter notebook
[I 20:36:46.487 NotebookApp] Serving notebooks from local directory: /Users/wangyu
[I 20:36:46.487 NotebookApp] The Jupyter Notebook is running at:
[I 20:36:46.487 NotebookApp] http://localhost:8888/?token=a192dc8378e5ca4162edf9b2a09125841cf3caee9d4c3c26
[I 20:36:46.487 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 20:36:46.491 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///Users/wangyu/Library/Jupyter/runtime/nbserver-56669-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=a192dc8378e5ca4162edf9b2a09125841cf3caee9d4c3c26
[I 20:36:56.627 NotebookApp] Kernel started: 09e0a361-cc1f-4840-b8a7-d57d1ca911b7
[I 20:36:57.768 NotebookApp] Adapting to protocol v5.1 for kernel 09e0a361-cc1f-4840-b8a7-d57d1ca911b7
[I 20:38:56.595 NotebookApp] Saving file at /VUML 2019/Untitled.ipynb
```



等待打开默认浏览器（safari）后出现下图

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311Miniconda3/Screen%20Shot%202019-03-11%20at%208.43.24%20PM.png)

当且仅当右上角Python3右边是个空心圆（而非一个断开的链接符号🔗）

才表示jupyter已经connected to kernel且可以正常使用



测试后显示kernel可以正常使用

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311Miniconda3/Screen%20Shot%202019-03-11%20at%2010.27.00%20PM.png)



## Summary

1. 网络资料种类多/信息杂乱，一定要先从terminal的报错/返回信息中寻找错误原因，再针对错误原因进行检索。
2. 不要盲目尝试，除非你可以记录下每一步的过程，有可供回退的log（但仍然很多软件无法回退旧版本）。尝试请慎重，但也不要畏手畏脚，大不了就是重装一次。
3. 有时表面看到的路径只是result，不是actual position，所以需要show package以真正进到安装目录，查看所需的安装信息。
4. 删除任何内容前请备份！！！！！！！如出现任何问题，backup可帮助回到前一状态。
5. CSDN虽说是中文，但有些问题背景描述不清，容易产生歧义。多在github上找答案，issue中的问题和回答虽然篇幅较长，但大多有价值。
6. Coding这类工作在成功那一秒所带来的巨大满足感是任何其他学习/工作都无法给予的。
7. 善于specify/clarify问题，也要善于寻找similarity/dependency。
8. 自己问题自己解决，别人不知道你的系统和环境，自己查资料才有用。
9. 解决问题的过程，也就是我们常说的 problem-solving skill，是需要长期训练和多次反复踩坑提炼出来的。训练所得技能和经验是自己的，没人代替得了你的努力和时间。
10. 善于利用搜索引擎 🔍（google, csdn, github, stack overflow），对照已有问题及答案解决当下问题，学会从返回信息中找问题。



##Appendix

安装jupyter 的重要内容1

```bash
Requirement already satisfied: pyrsistent>=0.14.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat>=4.4->nbconvert->jupyter) (0.14.11)

```

安装jupyter 的重要内容2

```bash
Installing collected packages: jupyter-core, nbformat, nbconvert, jupyter-client, ipykernel, notebook, ipywidgets, jupyter-console, jupyter
Successfully installed ipykernel-5.1.0 ipywidgets-7.4.2 jupyter-1.0.0 jupyter-client-5.2.4 jupyter-console-6.0.0 jupyter-core-4.4.0 nbconvert-5.4.1 nbformat-4.4.0 notebook-5.7.6
```



安装jupyter的全部terminal 返回过程：

```
Collecting jupyter
  Using cached https://files.pythonhosted.org/packages/83/df/0f5dd132200728a86190397e1ea87cd76244e42d39ec5e88efd25b2abd7e/jupyter-1.0.0-py2.py3-none-any.whl
Collecting nbconvert (from jupyter)
  Using cached https://files.pythonhosted.org/packages/b8/39/1e67fea74dc9577cc49f9863fe3ec824e525d1304ab6027d95a94cd586f5/nbconvert-5.4.1-py2.py3-none-any.whl
Collecting ipykernel (from jupyter)
  Using cached https://files.pythonhosted.org/packages/d8/b0/f0be5c5ab335196f5cce96e5b889a4fcf5bfe462eb0acc05cd7e2caf65eb/ipykernel-5.1.0-py3-none-any.whl
Collecting notebook (from jupyter)
  Downloading https://files.pythonhosted.org/packages/0a/d8/4e9521354ed3d730ba6d8a5af440b66c73245ef46be706e51bead71afc21/notebook-5.7.6-py2.py3-none-any.whl (9.0MB)
    100% |████████████████████████████████| 9.0MB 2.1MB/s
Requirement already satisfied: qtconsole in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jupyter) (4.4.3)
Collecting ipywidgets (from jupyter)
  Using cached https://files.pythonhosted.org/packages/30/9a/a008c7b1183fac9e52066d80a379b3c64eab535bd9d86cdc29a0b766fd82/ipywidgets-7.4.2-py2.py3-none-any.whl
Collecting jupyter-console (from jupyter)
  Using cached https://files.pythonhosted.org/packages/cb/ee/6374ae8c21b7d0847f9c3722dcdfac986b8e54fa9ad9ea66e1eb6320d2b8/jupyter_console-6.0.0-py2.py3-none-any.whl
Requirement already satisfied: pygments in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (2.3.1)
Requirement already satisfied: pandocfilters>=1.4.1 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (1.4.2)
Requirement already satisfied: jinja2 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (2.10)
Collecting jupyter-core (from nbconvert->jupyter)
  Using cached https://files.pythonhosted.org/packages/1d/44/065d2d7bae7bebc06f1dd70d23c36da8c50c0f08b4236716743d706762a8/jupyter_core-4.4.0-py2.py3-none-any.whl
Requirement already satisfied: bleach in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (3.1.0)
Requirement already satisfied: traitlets>=4.2 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (4.3.2)
Requirement already satisfied: mistune>=0.8.1 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (0.8.4)
Collecting nbformat>=4.4 (from nbconvert->jupyter)
  Using cached https://files.pythonhosted.org/packages/da/27/9a654d2b6cc1eaa517d1c5a4405166c7f6d72f04f6e7eea41855fe808a46/nbformat-4.4.0-py2.py3-none-any.whl
Requirement already satisfied: testpath in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (0.4.2)
Requirement already satisfied: entrypoints>=0.2.2 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (0.3)
Requirement already satisfied: defusedxml in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbconvert->jupyter) (0.5.0)
Requirement already satisfied: ipython>=5.0.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipykernel->jupyter) (7.3.0)
Requirement already satisfied: tornado>=4.2 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipykernel->jupyter) (6.0)
Collecting jupyter-client (from ipykernel->jupyter)
  Using cached https://files.pythonhosted.org/packages/3b/c3/3043fe9ffd140d03c9d091a056794ccdc427c56ec19b8eea74f9ea0a498f/jupyter_client-5.2.4-py2.py3-none-any.whl
Requirement already satisfied: prometheus-client in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from notebook->jupyter) (0.6.0)
Requirement already satisfied: ipython-genutils in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from notebook->jupyter) (0.2.0)
Requirement already satisfied: pyzmq>=17 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from notebook->jupyter) (18.0.0)
Requirement already satisfied: Send2Trash in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from notebook->jupyter) (1.5.0)
Requirement already satisfied: terminado>=0.8.1 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from notebook->jupyter) (0.8.1)
Requirement already satisfied: widgetsnbextension~=3.4.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipywidgets->jupyter) (3.4.2)
Requirement already satisfied: prompt-toolkit<2.1.0,>=2.0.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jupyter-console->jupyter) (2.0.9)
Requirement already satisfied: MarkupSafe>=0.23 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jinja2->nbconvert->jupyter) (1.1.1)
Requirement already satisfied: six>=1.9.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from bleach->nbconvert->jupyter) (1.12.0)
Requirement already satisfied: webencodings in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from bleach->nbconvert->jupyter) (0.5.1)
Requirement already satisfied: decorator in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from traitlets>=4.2->nbconvert->jupyter) (4.3.2)
Requirement already satisfied: jsonschema!=2.5.0,>=2.4 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from nbformat>=4.4->nbconvert->jupyter) (3.0.1)
Requirement already satisfied: backcall in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipython>=5.0.0->ipykernel->jupyter) (0.1.0)
Requirement already satisfied: pickleshare in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipython>=5.0.0->ipykernel->jupyter) (0.7.5)
Requirement already satisfied: pexpect; sys_platform != "win32" in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipython>=5.0.0->ipykernel->jupyter) (4.6.0)
Requirement already satisfied: setuptools>=18.5 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipython>=5.0.0->ipykernel->jupyter) (39.0.1)
Requirement already satisfied: appnope; sys_platform == "darwin" in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipython>=5.0.0->ipykernel->jupyter) (0.1.0)
Requirement already satisfied: jedi>=0.10 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from ipython>=5.0.0->ipykernel->jupyter) (0.13.3)
Requirement already satisfied: python-dateutil>=2.1 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jupyter-client->ipykernel->jupyter) (2.8.0)
Requirement already satisfied: ptyprocess; os_name != "nt" in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from terminado>=0.8.1->notebook->jupyter) (0.6.0)
Requirement already satisfied: wcwidth in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from prompt-toolkit<2.1.0,>=2.0.0->jupyter-console->jupyter) (0.1.7)
Requirement already satisfied: pyrsistent>=0.14.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat>=4.4->nbconvert->jupyter) (0.14.11)
Requirement already satisfied: attrs>=17.4.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat>=4.4->nbconvert->jupyter) (18.2.0)
Requirement already satisfied: parso>=0.3.0 in /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages (from jedi>=0.10->ipython>=5.0.0->ipykernel->jupyter) (0.3.4)
Installing collected packages: jupyter-core, nbformat, nbconvert, jupyter-client, ipykernel, notebook, ipywidgets, jupyter-console, jupyter
Successfully installed ipykernel-5.1.0 ipywidgets-7.4.2 jupyter-1.0.0 jupyter-client-5.2.4 jupyter-console-6.0.0 jupyter-core-4.4.0 nbconvert-5.4.1 nbformat-4.4.0 notebook-5.7.6
```



