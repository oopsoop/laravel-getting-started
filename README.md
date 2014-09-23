更多资料
https://github.com/huanghua581/laravel-getting-started/wiki

# Laravel 入门

本文介绍如何开始使用 Laravel。

读完本文，你将学到：  

* 如何安装 Laravel，新建 Laravel 程序，如何连接数据库；  
* Laravel 程序的基本文件结构；  
* MVC（模型，视图，控制器）和 REST 架构的基本原理；  
* 如何快速生成 Laravel 程序骨架；  

##1 前提条件
本文针对想从零开始开发 Laravel 程序的初学者，不需要预先具备任何的 Laravel 使用经验。不过，为了能顺利阅读，还是需要事先安装好一些软件：

* PHP 5.4 及以上版本
* 包管理工具 Composer 。想深入了解 Composer，请阅读 Composer 指南 。官网：https://getcomposer.org/ ， 中文网 ： http://www.phpcomposer.com/
* SQLite3 数据库

Laravel 是使用 PHP 语言开发的网页程序框架。如果之前没接触过 PHP，学习 Laravel 可要深下一番功夫。网上有很多资源可以学习 PHP：

PHP 语言官方网站： http://php.net/

##2 Laravel 是什么？
Laravel 是使用 PHP 语言编写的网页程序开发框架，目的是为开发者提供常用组件，简化网页程序的开发。只需编写较少的代码，就能实现其他编程语言或框架难以企及的功能。经验丰富的 PHP 程序员会发现，Laravel 让程序开发变得更有乐趣。

###Laravel 哲学

* Laravel 是一套富有表达性且具有简洁语法的网页应用程序框架。我们认为开发过程应该是愉悦且有创造性的体验。Laravel 努力减少开发过程中的不便，因此我们提供了验证(authentication)、路由(routing)、sessions、缓存(caching)等开发过程中经常用到的工具或功能。

* Laravel 目标是给开发者创造一个愉快的开发过程，并且不牺牲应用程序的功能性。快乐的开发者才能创造最棒的代码。为了这个目的，我们竭取了各框架的优点集中到 Laravel 中，这些框架包括并不局限于 Ruby on Rails、ASP.NET MVC 和 Sinatra 等。

* Laravel 是易于理解且强大的，它提供了强大的工具来开发大型、稳健的应用程序。杰出的 IoC、数据库迁移工具和紧密集成的单元测试，这些工具赋予您构建任何大小规模的应用程序的能力。

##3 新建 Laravel 程序
阅读本文时，最好跟着一步一步操作，如果错过某段代码或某个步骤，程序就可能出错，所以请一步一步跟着做。

本文会新建一个名为 blog 的 Laravel 程序，这是一个非常简单的博客。

> 文中的示例代码使用 $ 表示命令行提示符，你的提示符可能修改过，所以会不一样。在 Windows 中，提示符可能是 c:\source_code>。

###3.1 安装 Laravel
打开命令行：在 Mac OS X 中打开 Terminal.app，在 Windows 中选择“运行”，然后输入“cmd.exe”。下文中所有以 $ 开头的代码，都要在命令行中运行。先确认是否安装了 PHP 5.4 或者以上的版本：

> 有很多工具可以帮助你快速在系统中安装 PHP 。Windows 用户可以使用 WAMP，Mac OS X 用户可以使用 MAMP。

```
$ php -v    
PHP 5.4.10 (cli) (built: Jan 21 2013 15:12:32)  
Copyright (c) 1997-2012 The PHP Group  
Zend Engine v2.4.0, Copyright (c) 1998-2012 Zend Technologies  
     with XCache v2.0.1, Copyright (c) 2005-2012, by mOo  
```

如果你还没安装 PHP，请访问 http://php.net/ ，找到针对所用系统的安装方法。

很多类 Unix 系统都自带了版本尚新的 SQLite3。Windows 等其他操作系统的用户可以在 SQLite3 的网站上找到安装说明。然后，确认是否在 PATH 中：

```
$ sqlite3 --version
```

安装 Laravel , 通过 Laravel 安装器

首先, 使用 Composer 全局下载并安装 Laravel/installer:

```
$ composer global require "laravel/installer=~1.1"
```

请确定把 `~/.composer/vendor/bin` 路径放置于您的 PATH 里, 这样laravel 可执行文件才能被命令行找到, 以后您就可以在命令行下直接使用 laravel 命令.

安装并且配置成功后, 可以使用命令 `laravel new` 在您指定的目录下创建一份全新安装的 Laravel 应用, 如这样的调用: `laravel new blog` 将会在当前目录下创建一个叫 blog 的目录, 此目录里面存放着全新安装的 Laravel 应用, 此方法跟其他方法不一样的地方在于是提前安装好所有代码依赖的, 您无需再通过 `composer install` 安装, 速度一下子提高了很多.

Laravel 框架使用 composer 来执行安装及管理依赖。如果还没有安装它的话，请先从 安装 Composer 开始吧。

安装之后，您可以通过终端执行下列命令来安装 Laravel：

```
$ composer create-project laravel/laravel your-project-name --prefer-dist
```

这个命令会下载并安装一份全新的 Laravel 存放在指定的 your-project-name 的目录中。

> 如果您想要手动安装 Laravel 可以直接从 [Github 上的 Laravel Respoitory](https://github.com/laravel/laravel/archive/master.zip)下载一份代码。然后在解压后的根目录里，执行 composer install 即可，这个命令会把框架所需要的依赖下载完整。

###3.2 创建 Blog 程序
Artisan 是 Laravel 内建的命令行工具，它提供了一些有用的命令协助您开发，它是由强大的 Symfony Console 组件所驱动。

打开终端，进入有写权限的文件夹，执行以下命令生成一个新程序：

```
$ laravel new blog
```

或者

```
$ composer create-project laravel/laravel blog --prefer-dist
```

这个命令会在文件夹 blog 中新建一个 Laravel 程序。

> 执行 laravel new -h 可以查看新程序生成器的所有命令行选项。

生成 blog 程序后，进入该文件夹：  

```
$ cd blog  
```

blog 文件夹中有很多自动生成的文件和文件夹，组成一个 Laravel 程序。本文大部分时间都花在 app 文件夹上。下面简单介绍默认生成的文件和文件夹的作用：

文件/文件夹 | 作用  
----- | -----  
app/ | 包含了站点的 controllers（控制器），models（模型），views（视图）和 assets（资源）。这些是网站运行的主要代码，你会将你大部分的时间花在这些上面。本文主要关注的是这个文件夹。
bootstrap | 用来存放系统启动时需要的文件，这些文件会被如 index.php 这样的文件调用。
public | 这个文件夹是唯一外界可以看到的，是必须指向你 web 服务器的目录。它含有 laravel 框架核心的引导文件 index.php，这个目录也可用来存放任何可以公开的静态资源，如 css，Javascript，images 等。
vendor | 用来存放所有的第三方代码，在一个典型的 Laravel 应用程序，这包括 Laravel 源代码及其相关，并含有额外的预包装功能的插件。
app/config/ | 配置应用程序的运行时规则、 数据库、 session等等。包含大量的用来更改框架的各个方面的配置文件。大部分的配置文件中返回的选项关联PHP数组。
app/config/app.php | 各种应用程序级设置，即时区、 区域设置（语言环境）、 调试模式和独特的加密密钥。
app/config/auth.php | 控制在应用程序中如何进行身份验证，即身份验证驱动程序。
app/config/cache.php | 如果应用程序利用缓存来加快响应时间，要在此配置该功能。
app/config/compile.php | 在此处可以指定一些额外类，去包含由‘artisan optimize’命令声称的编译文件。这些应该是被包括在基本上每个请求到应用程序中的类。
app/config/database.php | 包含数据库的相关配置信息，即默认数据库引擎和连接信息。
app/config/mail.php | 为电子邮件发件引擎的配置文件，即 SMTP 服务器，From:标头
app/config/session.php | 控制Laravel怎样管理用户sessions,即session driver, session lifetime。
app/config/view.php | 模板系统的杂项配置。
app/controllers | 包含用于提供基本的逻辑、 数据模型交互以及加载应用程序的视图文件的控制器类。
app/database/migrations/ | 包含一些 PHP 类，允许 Laravel更新当前数据库的架构并同时保持所有版本的数据库的同步。迁移文件是使用Artisan工具生成的。
app/database/seeds/ | 包含允许Artisan工具用关系数据来填充数据库表的 PHP 文件。
app/lang/ | PHP 文件，其中包含使应用程序易于本地化的字符串的数组。默认情况下目录包含英语语言的分页和表单验证的语言行。
app/models/ | 模型是代表应用程序的信息（数据）和操作数据的规则的一些类。在大多数情况下，数据库中的每个表将对应应用中的一个模型。应用程序业务逻辑的大部分将集中在模型中。
app/start/ | 包含与Artisan工具以及全球和本地上下文相关的自定义设置。
app/storage/ |该目录存储Laravel各种服务的临时文件，如session, cache,  compiled view templates。这个目录在web服务器上必须是可以写入的。该目录由Laravel维护，我们可以不关心。
app/tests/ | 该文件夹给你提供了一个方便的位置，用来做单元测试。如果你使用PHPUnit，你可以使用Artisan工具一次执行所有的测试。
app/views/ | 该文件夹包含了控制器或者路由使用的HTML模版。请注意，这个文件夹下你只能放置模版文件。其他的静态资源文件如css, javascript和images文件应该放在/public文件夹下。
app/routes.php | 这是您的应用程序的路由文件，其中包含路由规则，告诉 Laravel 如何将传入的请求连接到路由处理的闭包函数、 控制器和操作。该文件还包含几个事件声明，包括错误页的，可以用于定义视图的composers。
app/filters.php | 此文件包含各种应用程序和路由筛选方法，用来改变您的应用程序的结果。Laravel 具有访问控制和 XSS 保护的一些预定义筛选器。

##4 Hello, Laravel!
首先，我们来添加一些文字，在页面中显示。为了能访问网页，要启动程序服务器。

```
$ php artisan serve
```

上述命令会启动 PHP 内建的开发服务器，要查看程序，请打开一个浏览器窗口，访问 http://localhost:8000 。应该会看到默认的 Laravel 信息页面：

![](http://drp.io/files/540e55b3bfde6.png)

> 要想停止服务器，请在命令行中按 Ctrl+C 键。服务器成功停止后回重新看到命令行提示符。在大多数类 Unix 系统中，包括 Mac OS X，命令行提示符是 $ 符号。

###4.2 显示“Hello, Laravel!”
要在 Laravel 中显示“Hello, Laravel!”，需要新建一个控制器和视图。

控制器用来接受向程序发起的请求。路由决定哪个控制器会接受到这个请求。一般情况下，每个控制器都有多个路由，对应不同的动作。动作用来提供视图中需要的数据。

视图的作用是，以人类能看懂的格式显示数据。有一点要特别注意，数据是在控制器中获取的，而不是在视图中。视图只是把数据显示出来。默认情况下，视图使用 Blade 编写，经由 Laravel 解析后，再发送给用户。

控制器可用控制器生成器创建，你要告诉生成器，我想要个名为“welcome”的控制器，如下所示：

```
$ php artisan controller:make WelcomeController --only=index
```

运行上述命令后，Laravel 会生成 app/controllers/WelcomeController.php 文件。生成文件后修改其中的 index 方法： 

```
	public function index()
	{
		return View::make('welcome.index');
	}
```

**创建视图： **    

* 在 app/views/ 目录新建文件夹 welcome 并创建文件 index.blade.php ;  
* 在 index.blade.php 文件中添加 `<h1>Hello, Laravel!</h1>` ;

###4.3 设置程序的首页
我们已经创建了控制器和视图，现在要告诉 Laravel 在哪个地址上显示“Hello, Laravel!”。这里，我们希望访问根地址 http://localhost:8000 时显示。但是现在显示的还是欢迎页面。

我们要告诉 Laravel 真正的首页是什么。

在编辑器中打开 app/routes.php 文件。

```
<?php

/*
|--------------------------------------------------------------------------
| Application Routes
|--------------------------------------------------------------------------
|
| Here is where you can register all of the routes for an application.
| It's a breeze. Simply tell Laravel the URIs it should respond to
| and give it the Closure to execute when that URI is requested.
|
*/

Route::get('/', function()
{
	return View::make('hello');
});
```

我们找到 ：

```
Route::get('/', function()
{
	return View::make('hello');
});
```

修改为：

```
Route::get('/', 'WelcomeController@index');
```

告知 Laravel，访问程序的根路径时，交给 welcome 控制器中的 index 动作处理。

##5 开始使用
前文已经介绍如何创建控制器、动作和视图，下面我们来创建一些更实质的功能。

**在此之前我们需要修改一些配置：**

* app/config/app.php 文件中的 debug 选项设置为 true （注：开启开发模式，更友好的开发提示）；
* app/config/database.php 文件中的 default 选项设置为 sqlite （注：我们之前选择 sqlite 作为默认数据库）；

在博客程序中，我们要创建一个新“资源”。资源是指一系列类似的对象，比如文章，人和动物。

资源可以被创建、读取、更新和删除，这些操作简称 CRUD。

Laravel 提供了资源控制器可以简单的建立跟资源相关的 RESTful 控制器。
创建文章资源后，app/routes.php 文件的内容新增如下：

```
Route::resource('articles', 'ArticlesController');
```

执行 `$ php artisan routes` 任务，会看到定义了所有标准的 REST 动作。输出结果中各列的意义稍后会说明。

``` 
+--------+-----------------------------------+------------------+----------------------------+----------------+---------------+
| Domain | URI                               | Name             | Action                     | Before Filters | After Filters |
+--------+-----------------------------------+------------------+----------------------------+----------------+---------------+
|        | GET|HEAD /                        |                  | WelcomeController@index    |                |               |
|        | GET|HEAD articles                 | articles.index   | ArticlesController@index   |                |               |
|        | GET|HEAD articles/create          | articles.create  | ArticlesController@create  |                |               |
|        | POST articles                     | articles.store   | ArticlesController@store   |                |               |
|        | GET|HEAD articles/{articles}      | articles.show    | ArticlesController@show    |                |               |
|        | GET|HEAD articles/{articles}/edit | articles.edit    | ArticlesController@edit    |                |               |
|        | PUT articles/{articles}           | articles.update  | ArticlesController@update  |                |               |
|        | PATCH articles/{articles}         |                  | ArticlesController@update  |                |               |
|        | DELETE articles/{articles}        | articles.destroy | ArticlesController@destroy |                |               |
+--------+-----------------------------------+------------------+----------------------------+----------------+---------------+

```

下一节，我们会加入新建文章和查看文章的功能。这两个操作分别对应于 CRUD 的 C 和 R，即创建和读取。

###5.1 挖地基
首先，程序中要有个页面用来新建文章。一个比较好的选择是 /articles/create。这个路由前面已经定义了，可以访问。打开 http://localhost:8000/articles/create ，会看到如下的路由错误：

![](http://drp.io/files/540e5636b9bd5.png)

产生这个错误的原因是，没有定义用来处理该请求的控制器。解决这个问题的方法很简单：创建名为 ArticlesController 的控制器。执行下面的命令即可：

```
$ php artisan controller:make ArticlesController
```

打开刚生成的 app/controllers/ArticlesController.php 文件，控制器就是一个类，继承自 BaseController。在这个 ArticlesController 类中定义了对应的资源动作。动作的作用是处理文章的 CRUD 操作。

修改 ArticlesController.php 文件中的 

```
	public function create()
	{
		//
	}
```

为

```
	public function create()
	{
		return View::make('articles.create');
	}
```

> 在 PHP 中，方法分为 public、private 和 protected 三种，只有 public 方法才能作为控制器的动作。

现在刷新 http://localhost:8000/articles/create ，会看到一个新错误：

![](http://drp.io/files/540e56a82547b.png)

产生这个错误的原因是，Laravel 希望这样的常规动作有对应的视图，用来显示内容。没有视图可用，Laravel 就报错了。

新建文件 app/views/articles/create.blade.php，写入如下代码：

```
<h1>New Article</h1>
```

再次刷新 http://localhost:8000/articles/create ， 可以看到页面中显示了一个标头。现在路由、控制器、动作和视图都能正常运行了。接下来要编写新建文章的表单了。

###5.2 首个表单
要在模板中编写表单，可以使用“表单构造器”。Laravel 中常用的表单构造器是 `Form`。在 app/views/articles/create.blade.php 文件中加入以下代码：

```
{{ Form::open() }}
    <p>
        {{ Form::text('title') }}
    </p>
    <p>
        {{ Form::text('text') }}
    </p>
    <p>
        {{ Form::submit('submit') }}
    </p>
{{ Form::close() }}
```

现在刷新页面，会看到上述代码生成的表单。在 Laravel 中编写表单就是这么简单！

在 Form 方法的块中，Form::text 创建了两个标签和两个文本字段，一个用于文章标题，一个用于文章内容。最后，Form::submit 创建一个提交按钮。

不过这个表单还有个问题。如果查看这个页面的源码，会发现表单 action 属性的值是 /articles/create。这就是问题所在，因为其指向的地址就是现在这个页面，而这个页面是用来显示新建文章表单的。

要想转到其他地址，就要使用其他的地址。这个问题可使用 Form::open 方法的 url 参数解决。在 Laravel 中，用来处理新建资源表单提交数据的动作是 store，所以表单应该转向这个动作。

修改 app/views/articles/create.blade.php 文件中的 Form::open，改成这样：

```
{{ Form::open(array('url' => 'articles')) }}
```

这里，我们把 url 参数的值设为 articles 。对应的地址是 /articels，默认情况下，这个表单会向这个路由发起 POST 请求。这个路由对应于 ArticlesController 控制器的 store 动作。

表单写好了，路由也定义了，现在可以填写表单，然后点击提交按钮新建文章了。

###5.3 创建文章
提交表单，会看到一个白屏。现在暂且不管这个错误。store 动作的作用是把新文章保存到数据库中。

提交表单后，其中的字段以参数的形式传递给 Laravel。这些参数可以在控制器的动作中使用，完成指定的操作。要想查看这些参数的内容，可以把 store 动作改成：

```
	public function store()
	{
		dd(Input::all());
	}
```

dd 函数为 Laravel 内置的打印输出函数，Input::all() 取得所有发出请求时传入的输入数据。

如果现在再次提交表单，不会再看到白屏错误，而是会看到类似下面的文字：

```
array (size=3)
  '_token' => string 'plx6TrGRWfHakBlKybUzkRTH8r712JU4rWfiPTs7' (length=40)
  'title' => string 'First article!' (length=14)
  'text' => string 'This is my first article.' (length=25)
```

store 动作把表单提交的参数显示出来了。不过这么做没什么用，看到了参数又怎样，什么都没发生。

###5.4 创建 Article 模型

在 Laravel 中，模型的名字使用单数，对应的数据表名使用复数。

创建 app/models/Article.php 并写入以下代码：

```
<?php

class Article extends Eloquent {

}
```

注意我们并没有告诉 Eloquent Article 模型会使用哪个数据库表。若没有特别指定，系统会默认自动对应名称为「类名称的小写复数形态」的数据库表。所以，在上面的例子中， Eloquent 会假设 Article 将把数据存在 articles 数据库表。

###5.5 运行迁移
使用 Artisan CLI 的 migrate:make 命令建立迁移文件：

```
$ php artisan migrate:make create_articles_table --create=articles
```

迁移文件会建立在 app/database/migrations 目录下，文件名会包含时间戳，用于在执行迁移时用来决定顺序。

app/database/migrations/2014_09_03_084339_create_articles_table.php （你的迁移文件名可能有点不一样）文件的内容如下所示：

```
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateArticlesTable extends Migration {

	/**
	 * Run the migrations.
	 *
	 * @return void
	 */
	public function up()
	{
		Schema::create('articles', function(Blueprint $table)
		{
			$table->increments('id');
			$table->timestamps();
		});
	}

	/**
	 * Reverse the migrations.
	 *
	 * @return void
	 */
	public function down()
	{
		Schema::drop('articles');
	}

}
```

修改其中的创建代码为：

```
		Schema::create('articles', function(Blueprint $table)
		{
			$table->increments('id');
			$table->string('title');
			$table->text('text');
			$table->timestamps();
		});
```

在这个迁移中定义了一个名为 up 的方法，在运行迁移时执行。up 方法中定义的操作都是可以通过 down 方法实现可逆的，Laravel 知道如何撤销这次迁移操作。运行迁移后，会创建 articles 表，以及一个字符串字段和文本字段。同时还会创建两个时间戳字段，用来跟踪记录的创建时间和更新时间。

然后，使用 Artisan 命令运行迁移：

```
$ php artisan migrate
```

Laravel 会执行迁移操作，告诉你创建了 articles 表。

> Migration table created successfully.
> Migrated: 2014_09_03_084339_create_articles_table

###5.6 在控制器中保存数据

再回到 ArticlesController 控制器，我们要修改 store 动作，使用 Article 模型把数据保存到数据库中。打开 app/controllers/ArticlesController.php 文件，把 store 动作修改成这样：

```
	public function store()
	{
        	$article = Article::create(array('title'=>Input::get('title'), 'text'=>Input::get('text')));

		return Redirect::route('articles.show', array($article->id));
	}
```

同时在 app/models/Article.php 添加 ：

```
protected $fillable = array('title', 'text');
```

fillable 属性允许在动作中调用模型的 create 方法使用 title 和 text 属性。

再次访问 http://localhost:8000/articles/create ，填写表单，还差一步就能创建文章了。

###5.7 显示文章
和前面一样，我们要在 app/controllers/ArticlesController.php 文件中更改 show 动作，以及相应的视图文件。

```
	public function show($id)
	{
		$article = Article::find($id);

		return View::make('articles.show', compact('article'));
	}
```

然后，新建 app/views/articles/show.blade.php 文件，写入下面的代码：



```
<p>
  <strong>Title:</strong>
  {{ $article->title }}
</p>

<p>
  <strong>Text:</strong>
  {{ $article->text }}
</p>
```

做了以上修改后，就能真正的新建文章了。访问 http://localhost:8000/articles/create ，自己试试。

###5.8 列出所有文章
我们还要列出所有文章，对应的路由是：

>  GET|HEAD articles                 | articles.index   | ArticlesController@index

在 app/controllers/ArticlesController.php 文件中，修改 ArticlesController 控制器 index 动作：

```
	public function index()
	{
		$articles = Article::all();

		return View::make('articles.index', compact('articles'));
	}
```

然后编写这个动作的视图，保存为 app/views/articles/index.blade.php：


```
<h1>Listing articles</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
  </tr>

  @foreach ($articles as $article)
    <tr>
      <td>{{ $article->title }}</td>
      <td>{{ $article->text }}</td>
    </tr>
  @endforeach
</table>
```


现在访问 http://localhost:8000/articles ，会看到已经发布的文章列表。

###5.9 添加链接

至此，我们可以新建、显示、列出文章了。下面我们添加一些链接，指向这些页面。

打开 app/views/welcome/index.blade.php 文件，添加：

```  
{{ link_to_route('articles.index', 'My Blog') }} 
```

link_to_route 是 Laravel 内置的视图帮助方法之一，根据提供的文本和地址创建超链接。这上面这段代码中，地址是文章列表页面。

接下来添加到其他页面的链接。先在 app/views/articles/index.blade.php 中添加“New Article”链接，放在 <table> 标签之前：

```
{{ link_to_route('articles.create', 'New article') }}
```

点击这个链接后，会转向新建文章的表单页面。

然后在 app/views/articles/create.blade.php 中添加一个链接，位于表单下面，返回到 index 动作：

```
{{ link_to_route('articles.index', 'Back') }}
```

最后，在 app/views/articles/show.blade.php 模板中添加一个链接，返回 index 动作，这样用户查看某篇文章后就可以返回文章列表页面了：

```
{{ link_to_route('articles.index', 'Back') }}
```

###5.10 添加数据验证

在 app/controllers/ArticlesController.php 文件中，修改 ArticlesController 控制器 store 动作：

```
	public function store()
	{
		$rules = array('title' => 'required|min:5');

		$validator = Validator::make(Input::all(), $rules);

        if ($validator->fails())
        {
            return Redirect::route('articles.create')
                ->withErrors($validator)
                ->withInput();
        }

        $article = Article::create(array('title'=>Input::get('title'), 'text'=>Input::get('text')));

		return Redirect::route('articles.show', array($article->id));
	}
```

然后修改  app/views/articles/create.blade.php 添加 ：

```
@if ($errors->any())
<div id="error_explanation">
    <h2>{{ count($errors->all()) }} prohibited
      this article from being saved:</h2>
    <ul>
    @foreach ($errors->all() as $message)
      <li>{{ $message }}</li>
    @endforeach
    </ul>
  </div>
@endif
```

再次访问 http://localhost:8000/articles/create ，尝试发布一篇没有标题的文章，会看到一个很有用的错误提示。

###5.11 更新文章

我们已经说明了 CRUD 中的 CR 两种操作。下面进入 U 部分，更新文章。

首先，要在 ArticlesController 中更改 edit 动作：

```
	public function edit($id)
	{
		$article = Article::find($id);

		return View::make('articles.edit', compact('article'));
	}
```

视图中要添加一个类似新建文章的表单。新建 app/views/articles/edit.blade.php  文件，写入下面的代码：

```
<h1>Editing Article</h1>

@if ($errors->any())
<div id="error_explanation">
    <h2>{{ count($errors->all()) }} prohibited
      this article from being saved:</h2>
    <ul>
    @foreach ($errors->all() as $message)
      <li>{{ $message }}</li>
    @endforeach
    </ul>
  </div>
@endif

{{ Form::open(array('route' => array('articles.update', $article->id), 'method' => 'put')) }}
    <p>
        {{ Form::text('title', $article->title) }}
    </p>
    <p>
        {{ Form::text('text', $article->text) }}
    </p>
    <p>
        {{ Form::submit('submit') }}
    </p>
{{ Form::close() }}

{{ link_to_route('articles.index', 'Back') }}
```

这里的表单指向 update 动作

method: put ( patch ) 选项告诉 Laravel，提交这个表单时使用 PUT 方法发送请求。根据 REST 架构，更新资源时要使用 HTTP PUT 方法。

然后，要在 app/controllers/ArticlesController.php 中更新 update 动作：

```
	public function update($id)
	{
		$rules = array('title' => 'required|min:5');

		$validator = Validator::make(Input::all(), $rules);

        if ($validator->fails())
        {
            return Redirect::route('articles.create')
                ->withErrors($validator)
                ->withInput();
        }

		$article = Article::find($id);

		$article->title = Input::get('title');
		$article->text = Input::get('text');
		$article->save();

		return Redirect::route('articles.show', array($article->id));
	}
```

最后，我们想在文章列表页面，在每篇文章后面都加上一个链接，指向 edit 动作。打开 app/views/articles/index.blade.php 文件，在“Show”链接后面添加“Edit”链接：

```
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th colspan="2"></th>
  </tr>

  @foreach ($articles as $article)
    <tr>
      <td>{{ $article->title }}</td>
      <td>{{ $article->text }}</td>
      <td>{{ link_to_route('articles.show', 'Show', $article->id) }}</td>
      <td>{{ link_to_route('articles.edit', 'Edit', $article->id) }}</td>
    </tr>
  @endforeach
</table>
```

我们还要在 app/views/articles/show.blade.php 模板的底部加上“Edit”链接：

```
{{ link_to_route('articles.index', 'Back') }} |
{{ link_to_route('articles.edit', 'Edit', $article->id) }}
```

###5.12 使用局部视图去掉视图中的重复代码

编辑文章页面和新建文章页面很相似，显示错误提示的代码是相同的。下面使用局部视图去掉两个视图中的重复代码。

新建 app/views/notifications.blade.php 文件，写入以下代码：

```
@if ($errors->any())
<div id="error_explanation">
    <h2>{{ count($errors->all()) }} prohibited
      this article from being saved:</h2>
    <ul>
    @foreach ($errors->all() as $message)
      <li>{{ $message }}</li>
    @endforeach
    </ul>
  </div>
@endif
```

下面来修改 app/views/articles/creat.blade.php 和 edit.blade.php  视图，使用新建的局部视图，把其中的上面代码全删掉，替换成：

```
@include('notifications')
```

###5.13 删除文章

现在介绍 CRUD 中的 D，从数据库中删除文章。按照 REST 架构的约定，删除文章的路由是：

> DELETE articles/{articles}        | articles.destroy | ArticlesController@destroy

删除资源时使用 DELETE 请求。如果还使用 GET 请求，可以构建如下所示的恶意地址：

```
<a href='http://example.com/articles/1/destroy'>look at this cat!</a>
```

删除资源使用 DELETE 方法，路由会把请求发往 app/controllers/ArticlesController.php 中的 destroy 动作。修改 destroy 动作：

```
	public function destroy($id)
	{
		Article::destroy($id);

		return Redirect::route('articles.index');
	}
```

想把记录从数据库删除，可以在模型对象上调用 destroy 方法。注意，我们无需为这个动作编写视图，因为它会转向 index 动作。

最后，在 index 动作的模板（app/views/articles/index.blade.php）中加上“Destroy”链接：

```
<table>
  <tr>
    <th>Title</th>
    <th>Text</th>
    <th colspan="2"></th>
  </tr>

  @foreach ($articles as $article)
    <tr>
      <td>{{ $article->title }}</td>
      <td>{{ $article->text }}</td>
      <td>{{ link_to_route('articles.show', 'Show', $article->id) }}</td>
      <td>{{ link_to_route('articles.edit', 'Edit', $article->id) }}</td>
      <td>
        {{ Form::open(array('method' => 'DELETE', 'route' => array('articles.destroy', $article->id))) }}
          {{ Form::submit('Delete') }}
        {{ Form::close() }}
      </td>
    </tr>
  @endforeach
</table>
```

恭喜，现在你可以新建、显示、列出、更新、删除文章了。


##接下来做什么
至此，我们开发了第一个 Laravel 程序，请尽情的修改、试验。在开发过程中难免会需要帮助，如果使用 Laravel 时需要协助，可以使用这些资源：

* http://laravel.com/
* http://golaravel.com/
* http://laravel-china.org/

##常见问题
使用 Laravel 时，最好使用 UTF-8 编码存储所有外部数据。

如果编码出错，常见的征兆是浏览器中显示很多黑色方块和问号。还有一种常见的符号是“Ã¼”，包含在“ü”中。

非 UTF-8 编码的数据经常来源于：

* 你的文本编辑器：大多数文本编辑器（例如 TextMate）默认使用 UTF-8 编码保存文件。如果你的编辑器没使用 UTF-8 编码，有可能是你在模板中输入了特殊字符（例如 é），在浏览器中显示为方块和问号。这种问题也会出现在国际化文件中。默认不使用 UTF-8 保存文件的编辑器（例如 Dreamweaver 的某些版本）都会提供一种方法，把默认编码设为 UTF-8。记得要修改。
* 你的数据库：默认情况下，Laravel 会把从数据库中取出的数据转换成 UTF-8 格式。如果数据库内部不使用 UTF-8 编码，就无法保存用户输入的所有字符。例如，数据库内部使用 Latin-1 编码，用户输入俄语、希伯来语或日语字符时，存进数据库时就会永远丢失。如果可能，在数据库中尽量使用 UTF-8 编码。

##反馈
欢迎帮忙改善文档质量。

直接 issues 吧！

##License

[![Creative Commons License](http://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
