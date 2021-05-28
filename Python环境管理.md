## 检查conda

在使用conda前，我们先检查conda是否已经被安装，以及当前版本是否是最新。

```python
# 检查conda是否已经安装好，此命令会返回你安装Anaconda软件的版本
conda --version
>> conda 4.3.40

# 通过以下命令升级conda到最新版本
# 如果有新版本可用，在提示proceed ([y]/n)? 中输入y进行升级
conda update conda
```

## 环境管理

环境管理是Python使用中的一大好习惯，如果你不想在一遍遍重装Python和系统中折腾循，那么环境管理是学习Python的过程中非常必要的一环。现在我们用conda进行环境管理。

**创建环境**

```python
# 创建一个环境名为py34，指定Python版本是3.4
#（不用管是3.4.x，conda会为我们自动寻找3.4.x中的最新版本）
conda create --name py34 python=3.4
# 通过创建环境，我们可以使用不同版本的Python
conda create --name py27 python=2.7
```

**激活环境**

```python
# 在windows环境下使用activate激活
activate py34

# 在Linux & Mac中使用source activate激活
source activate py34
```

激活后，会发现terminal输入的地方多了(py34)的字样，这表示我们已经进入了py34的环境中。

**退出环境**

```python
# 在windows环境下使用deactivate
deactivate

# 在Linux & Mac中使用source deactivate
source deactivate
```

**删除环境**

如果你不想要这个名为py34的环境，可以通过以下命令删除这个环境。

```python
conda remove -n py34 --all
```

可以通过以下命令查看已有的环境列表，现在py34已经不在这个列表里，所以我们知道它已经被删除了。

```python
conda info -e
```

## 包管理

我们使用conda进行第三方包的安装、卸载和更新。

对于包的下载，我们可以先设置国内镜像。这是因为(http://Anaconda.org)的服务器在国外，所以conda在下载包的时候速度往往很慢。
所幸清华TUNA镜像（https://mirrors.tuna.tsinghua.edu.cn/help/anaconda)有Anaconda仓库的镜像，我们将其加入conda的配置，即可解决这个问题。

```python
# 添加Anaconda的TUNA镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```

接下来我们进行包的安装，请进入指定的环境中（比如上节中的py34），这里我们以pandas（一个数据处理和分析的包）为例进行操作。

**查看已安装的包**

```python
#使用这条命令来查看在当前环境中，已安装的包和对应版本
conda list
```

**查找可安装的包**

```python
#我们可以通过search命令检查pandas这个包是否可以通过conda来安装
#命令返回了这个包的信息，所以是可以通过conda安装的
conda search pandas
```

**安装包**

```python
#通过install安装pandas
#如果pandas已经存在于环境中，会提示已经安装，否则在提示proceed ([y]/n)? 中输入y进行安装
conda install pandas
```

**更新包**

```python
#通过update更新pandas
conda update pandas
```

**卸载包**

```python
#通过remove卸载pandas
conda remove pandas
```

以上就是conda对于包的安装、更新和卸载。值得一提的是，conda将conda、python等都视为包，因此，完全可以使用conda来管理conda和python的版本，例如

```python
# 更新conda到最新版本，这里conda被当作一个包处理 
conda update conda 

# 同样的，也可以更新anaconda到最新版本
conda update anaconda

# 更新python
# 例如我们所启用的环境是py34，使用的是python3.4,那么conda会将python升级为3.4.x系列中的最新版本
conda update python 
```
