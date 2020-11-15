# 准备工作 {- #ch0}

“工欲善其事，必先利其器。”

准备工作中常用的链接有

- [GitHub](https://github.com/JSchelldorfer/ActuarialDataScience)

- [Git](https://git-scm.com/)

- [SSH key](https://docs.github.com/cn/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh)

- [GitHub and RStudio](https://resources.github.com/whitepapers/github-and-rstudio/)

- [Jupyter Notebook](https://jupyter.org/)

- [Anaconda](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)

- [Miniconda](https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/?C=N&O=D)

- [TUNA镜像源](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

- [R interface to Tensorflow and Keras](https://keras.rstudio.com/)

- [reticulate](https://cran.r-project.org/web/packages/reticulate/)

- [Tensorflow](https://tensorflow.google.cn/)

- [Pytorch](https://pytorch.apachecn.org/)

- [校级计算云](https://cc.ruc.edu.cn/home)

- [CUDA](https://developer.nvidia.com/cuda-toolkit-archivE)

- [cuDNN](https://developer.nvidia.com/rdp/form/cudnn-download-survey)


## 克隆代码

[GitHub](https://github.com/)提供了大量开源代码，这门课的代码主要来自[此链接](https://github.com/JSchelldorfer/ActuarialDataScience)。通常，使用GitHub开源代码最方便的是`fork`到自己GitHub账户下，然后`clone`到本地。具体而言，需要进行以下操作：

1. 注册GitHub账户。

2. `Fork`[此链接](https://github.com/JSchelldorfer/ActuarialDataScience)到自己账户下的新仓库,可重新命名为如`Modern-Actuarial-Models`或其他名称。

3. 安装[git](https://git-scm.com/)。在命令窗口使用`$ git config --global user.name "Your Name"` 和 `$ git config --global user.email "youremail@yourdomain.com"` 配置git的用户名和邮箱分别为GitHub账户的用户名和邮箱。最后可使用`$ git config --list`查看配置信息。

4. (选做)在本地电脑创建ssh public key，并拷贝到GitHub中`Setting`下`SSH and GPG keys`。ssh public key一般保存在本人目录下的隐藏文件夹.ssh中，扩展名为.pub。详见[链接](https://docs.github.com/cn/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh)。设立SSH可以避免后续`push`代码到云端时，每次都需要输入密码的麻烦

5. 电脑连接手机4G热点。一般地，在手机4G网络下克隆的速度比较快。

6. 在RStudio中创建新的项目，选择Version Control，然后Git，在Repository URL中输入你的GitHub中刚才`fork`的新仓库地址（在`Code`下能找到克隆地址，如果第4步完成可以选择SSH地址，如果第4步没完成必须选择HTTPS地址），输入文件夹名称，选择存放位置，点击`create project`，RStudio开始克隆GitHub上该仓库的所有内容。 

7. 此时，你在GitHub上仓库的内容全部克隆到了本地，且放在了一个R Project中。在该Project中，会多两个文件，.Rproj和.gitignore，第一个文件保存了Project的设置，第二文件告诉git在`push`本地文件到GitHub时哪些文件被忽略。

8. 如果你修改了本地文件，可以通过R中内嵌的Git上传到GitHub（先`commit`再`push`），这样方便在不同电脑上同步文件。git是代码版本控制工具，在`push`之前，你可以比较和上个代码版本的差异。GitHub记录了你每次`push`的详细信息，且存放在本地文件夹.git中。同时，如果GitHub上代码有变化，你可以`pull`到本地。如果经常在不同电脑上使用本仓库，一般需要先`pull`成最新版本，然后再编辑修改，最后`commit-push`到GitHub。

9. (选做) 你可以建立新的`branch`，使自己的修改和源代码分开。具体操作可参考[链接](https://resources.github.com/whitepapers/github-and-rstudio/)，或者参考账户建立时自动产生的`getting-started`仓库。

10. (选做) 你可以尝试[Github Desktop](https://desktop.github.com/)或者[Jupyter Lab](https://jupyter.org/)（加载git extension）管理，但对于这门课，这两种方式不是最优。

理论上，GitHub上所有仓库都可以采用以上方法在RStudio中管理，当然，RStudio对于R代码仓库管理最有效，因为我们可以直接在RStudio中运行仓库中的代码。

## 建立环境

首先下载并安装[Anaconda](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)或者[Miniconda](https://docs.conda.io/en/latest/miniconda.html)。

以下步骤中，当你发现安装非常慢时，可以尝试4G网络，尝试VPN，尝试改变CRAN的镜像源，或尝试改变conda的镜像源。conda镜像源通过修改用户目录下的`.condarc`文件使用[TUNA镜像源](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)。

### R interface to Keras

这里主要说明`keras`包的安装和使用。[Keras](https://keras.rstudio.com/)是tensorflow的API，在keras中建立的神经网络模型都由tensorflow训练。安装`keras`包主要是安装Python库tensorflow，并让R与之相关联。

#### R自动安装

最简单的安装方式如下：

1. 使用`install.packages("tensorflow")`安装所有相关的包，然后`library("tensorflow")`。

2. `install_tensorflow()`

  这时大概率会出现

    No non-system installation of Python could be found.
    Would you like to download and install Miniconda?
    Miniconda is an open source environment management system for Python.
    See https://docs.conda.io/en/latest/miniconda.html for more details.
    Would you like to install Miniconda? [Y/n]:
  
  虽然你可能已经有Anaconda和Python，但R没有“智能”地识别出来，这时仍建议你点`Y`，让R自己装一下自己能更好识别的`Minicon   da`, 这个命令还会自动建立一个独立conda环境`r-reticulate`，并在其中装好`tensorflow, keras`等。
  
3. 上步如果正常运行，结束后会自动重启R。这时你运行`library(tensorflow)`然后`tf$constant("Hellow Tensorflow")`，如果没报错，那继续`install_packages("keras")`,`library("keras")`。

  用以下代码验证安装成功

    model <- keras_model_sequential() %>% 
    layer_flatten(input_shape = c(28, 28)) %>% 
    layer_dense(units = 128, activation = "relu") %>% 
    layer_dropout(0.2) %>% 
    layer_dense(10, activation = "softmax")
    summary(model)
    
  如果出现以下错误
  
    错误: Installation of TensorFlow not found.
    Python environments searched for 'tensorflow' package:
    C:\Users\Guangyuan\AppData\Local\r-miniconda\envs\r-reticulate\python.exe
    You can install TensorFlow using the install_tensorflow() function.
  
  抱歉！我暂时没找到解决办法。。。但我们可以在conda下安装好tensorflow然后关联到R，或者用其他方式让R找到其他方式安装的`tensorflow`。这时，你先把之前失败的安装`C:\Users\Guangyuan\AppData\Local\r-miniconda`，这个文件夹完全删掉。然后参考以下安装步骤。
  
#### 使用reticulate关联conda环境

1. 运行`Anaconda Prompt`或者`Anaconda Powershell Prompt`，在命令行输入`conda create -n r-tensorflow tensorflow`，conda会创建一个独立的`r-tensorflow`环境，并在其中安装`tensorflow`包。

2. 继续在命令行运行`conda activate r-tensorflow`加载刚刚安装的环境，并`pip install h5py pyyaml requests Pillow scipy`在该环境下安装keras依赖的包。至此，R需要的tensorflow环境已经准备好，接下来让R关联此环境。

3. 重启R，`library("reticulate")`然后`use_condaenv("r-tensorflow",required=T)`,这时R就和上面建立的环境关联好。

4. `library("keras“)`。这里假设你已经装好`tensorflow`和`keras`包。

  用以下代码验证安装成功

    model <- keras_model_sequential() %>% 
    layer_flatten(input_shape = c(28, 28)) %>% 
    layer_dense(units = 128, activation = "relu") %>% 
    layer_dropout(0.2) %>% 
    layer_dense(10, activation = "softmax")
    summary(model)
 
#### 指定conda安装

1. 命令行输入`which -a python`，找到Anaconda中Python的路径记为`anapy`。

2. R中`install_packages("tensorflow")`，然后

    install_tensorflow(method="conda",conda = "anapy",envname="r-tensorflow")
`
  此命令会在conda下创建`r-tensorflow`的环境并装好tensorflow包。
  
3. `install_packages("keras"); library("keras")`

  用以下代码验证安装成功

    model <- keras_model_sequential() %>% 
    layer_flatten(input_shape = c(28, 28)) %>% 
    layer_dense(units = 128, activation = "relu") %>% 
    layer_dropout(0.2) %>% 
    layer_dense(10, activation = "softmax")
    summary(model)

#### 使用reticulate安装

1. 重启R，`library("reticulate")`。

2. `options(timeout=300)`，防止下载时间过长中断。

3. `install_miniconda()`，将会安装`miniconda`并创建一个`r-reticulate`conda环境。此环境为R默认调用的Python环境。

4. （重启R）`library("tensorflow"); install_tensorflow()`，将会在`r-reticulate`安装`tensorflow`。

5. `install_packages("keras"); library("keras")`

  用以下代码验证安装成功

    model <- keras_model_sequential() %>% 
    layer_flatten(input_shape = c(28, 28)) %>% 
    layer_dense(units = 128, activation = "relu") %>% 
    layer_dropout(0.2) %>% 
    layer_dense(10, activation = "softmax")
    summary(model)

### R interface to Python

R包`reticulate`为`tensorflow`的依赖包，当你装`tensorflow`它也被自动安装。它可以建立R与Python的交互。

#### reticulate 常见命令

- `conda_list()`列出已安装的conda环境

- `virtualenv_list()`列出已存在的虚拟环境

- `use_python, use_condaenv, use_virtualenv`可以指定与R关联的python。

- `py_config()`可以查看当前Python关联信息。

很多时候，R会创建一个独立conda环境`r-miniconda/envs/r-reticulate`。

#### 切换R关联的conda环境

根据需要，你可以切换R关联的conda环境。具体步骤为

1. 重启R

2. `library("reticulate")`

3. `conda_list()`列出可以关联的环境和路径。

4. `use_condaenv("env-name")`。`env-name`为关联的conda环境。

5. `py_config`查看是否关联成功。

### Python

一般在每个Python（conda）环境都需要安装一个Jupyter Notebook方便使用该环境的科学计算包。

#### Conda环境

Python（conda）环境建立比较简单，在`使用reticulate关联conda环境`我们已经建立过一个环境`r-tensorflow`。具体操作如下:

1. 建立独立环境`conda create env -n env-name python=3.8 tensorflow notebook`。该命令会建立`env-name`的环境，并在其中安装`python=3.8`,`tensorflow`，`notebook`包及其依赖包。

2. 激活环境`conda activate env-name`.

3. cd 到你的工作目录。

4. 启动jupyter notebook `jupyter notebook`。

5. 如遇到缺少的包，在该环境`env-name`下使用`conda install ***`安装缺少的包。

#### Tensorflow/Pytorch GPU version

`Tensorflow`可以综合使用CPU和GPU进行计算，GPU的硬件结构适进行卷积运算，所以适于CNN，RNN等模型的求解。

你可以申请使用[校级计算云](https://cc.ruc.edu.cn/home)或者使用学院计算云，它们的服务器都配置了GPU，并装好了可以使用GPU的Tensorflow或者Pytorch。使用[校级计算云](https://cc.ruc.edu.cn/home)时，你通常只需要运行Jupyter Notebook就可以使用云端GPU进行计算。使用学院计算云时，你通常需要知道一些常用的[Linux命令](https://www.linuxcool.com/)，你也可以安装[Ubuntu](https://ubuntu.com/)来熟悉Linux系统。

[校级计算云](https://cc.ruc.edu.cn/home)和学院计算云有专门的IT人员帮你解决如本页所示的大部分IT问题。

你的机器如果有GPU，可以大致按如下步骤让GPU发挥它的并行计算能力，关键点是让GPU型号、CUDA版本、Tensorflow或Pytorch版本彼此匹配，且彼此“相连”。百度或者必应上有很多相关资料可以作为参考。

1.  查看电脑GPU，以及支持的[CUDA版本](https://developer.nvidia.com/cuda-gpus)。 或者在终端执行以下命令：nvidia-smi，查看你的NVIDIA显卡驱动支持的CUDA版本。

2. 查看各个[Tensorflow版本](https://tensorflow.google.cn/install/source?hl=zh-cn#linux)，[Pytorch版本](https://pytorch.org/get-started/locally/)对应的CUDA和cuDNN.

3. 下载并安装正确版本的[CUDA](https://developer.nvidia.com/cuda-toolkit-archivE)。注册、下载并安装正确版本的[cuDNN](https://developer.nvidia.com/rdp/form/cudnn-download-survey)

4. 配置CUDA和cuDNN.

5. 安装[Tensorflow](https://tensorflow.google.cn/install)或者[Pytorch](https://pytorch.org/get-started/locally/).
