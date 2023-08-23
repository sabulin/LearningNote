# 基于django的学习笔记系统（django框架简单练习）

简单的基于django开发的前后端分离web系统，使用python manage.py runserver运行

## 创建数据库
Django将大部分与项目相关的信息存储在数据库中，因此需要创建一个供Django使
用的数据库。为给项目“学习笔记”创建数据库，请在虚拟环境处于活动状态的情
况下执行下面的命令：
```shell
python manage.py migrate
```

## 查看项目
下面来核实Django正确地创建了项目。为此，可使用命令runserver 查看项目的
状态
```shell
python manage.py runserver
```

```shell
python manage.py startapp learning_logs
```
命令startapp appname 让Django搭建创建应用程序所需的基础设施。如果现在
查看项目目录，将看到其中新增了文件夹learning_logs。打开这个文件
夹，看看Django都创建了什么，其中最重要的文件是models.py、admin.py
和views.py。我们将使用models.py来定义要在应用程序中管理的数据，稍后再介绍
admin.py和views.py。

## 定义模型
我们来想想涉及的数据。每位用户都需要在学习笔记中创建很多主题。用户输入的
每个条目都与特定主题相关联，这些条目将以文本的方式显示。我们还需要存储每
个条目的时间戳，以便告诉用户各个条目都是什么时候创建的。
我们创建了一个名为Topic 的类，它继承Model ，即Django中定义了模型基本功
能的类。我们给Topic 类添加了两个属性：text 和date_added 。

## 激活模型
要使用这些模型，必须让Django将前述应用程序包含到项目中。为此，打开
settings.py

接下来，需要让Django修改数据库，使其能够存储与模型Topic 相关的信息。为
此，在终端窗口中执行下面的命令：
```shell
python manage.py makemigrations learning_logs
```
命令makemigrations 让Django确定该如何修改数据库，使其能够存储与前面定
义的新模型相关联的数据。输出表明Django创建了一个名为0001_initial.py的迁移
文件，这个文件将在数据库中为模型Topic 创建一个表。

下面应用这种迁移，让Django替我们修改数据库：
```shell
python manage.py migrate
```

**每当需要修改“学习笔记”管理的数据时，都采取如下三个步骤：修改models.py，
对learning_logs 调用makemigrations ，以及让Django迁移项目。**

## Django管理网站

### 创建超级用户
```shell
python manage.py createsuperuser
```
访问
http://localhost:8000/admin/，并输入刚创建的超级用户的用户名和密码。
你将看到类似于图18-2所示的屏幕。这个页面让你能够添加和修改用户和用户
组，还可管理与刚才定义的模型Topic 相关的数据。


## Django shell
输入一些数据后，就可通过交互式终端会话以编程方式查看这些数据了。这种交互
式环境称为Django shell ，是测试项目和排除故障的理想之地。
```shell
python manage.py shell
```

## 创建页面：学习笔记主页

### 映射URL
### 编写视图
### 编写模板

## 创建其他页面
制定创建页面的流程后，可以开始扩充“学习笔记”项目了。我们将创建两个显示
数据的页面，其中一个列出所有的主题，另一个显示特定主题的所有条目。对于每
个页面，我们都将指定URL模式、编写一个视图函数并编写一个模板。但这样做之
前，我们先创建一个父模板，项目中的其他模板都将继承它。
### 模板继承
创建网站时，一些通用元素几乎会在所有页面中出现。在这种情况下，可编写一个
包含通用元素的父模板，并让每个页面都继承这个模板，而不必在每个页面中重复
定义这些通用元素。这种方法能让你专注于开发每个页面的独特方面，还能让修改
项目的整体外观容易得多。

## 显示所有主题的页面

###  URL模式
定义显示所有主题的页面的URL

### 视图

### 模板


## 2. 用户账户

### 2.1 让用户输入数据
我们将使用Django的表单创建工具来创建让用户能够输入数据的页面

#### 添加新主题
用于添加主题的表单
让用户输入并提交信息的页面都是表单，那怕看起来不像。用户输入信息时，
我们需要进行验证，确认提供的信息是正确的数据类型，而不是恶意的信息，
如中断服务器的代码。然后，对这些有效信息进行处理，并将其保存到数据库
的合适地方。这些工作很多都是由Django自动完成的。
在Diango中，创建表单的最简单方式是使用ModelForm ，它根据我们定义的模型中的信息自动创建表单。

用于添加主题的表单
 URL模式new_topic
视图函数new_topic()
模板new_topic
链接到页面new_topic

### 2.2 创建用户账户

应用程序users
```shell
python manage.py startapp users
```
将users 添加到settings.py中

包含users 的URL
需要修改项目根目录中的urls.py，使其包含将为应用程序users 定义的URL

#### 登录页面
......