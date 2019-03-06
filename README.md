# jupyter-notebook
jupyter notebook
从工作开始接触Jupyter notebook，结合ipython来使用简直是爽，相见恨晚，不愧是python的一大利器，当然Jupyter notebook也支持别的语言，不过别的就不熟悉了，有一些notebook的使用技巧记录如下，希望更多的人能够从Jupyter notebook中像我一样获得更大的乐趣。 
参考： 
https://www.ishuo.cn/doc/kbrtriqf.html 
https://www.douban.com/review/7890354/ 
http://stackoverflow.com/questions/38318166/jupyter-notebook-output-image-in-previous-line/38320547 
https://github.com/ipython-contrib/jupyter_contrib_nbextensions

1.简介：
Jupyther notebook ,也就是一般说的 Ipython notebook，是一个可以把代码、图像、注释、公式和作图集于一处，从而实现可读性分析的一种灵活的工具。 
默认情况下，Jupyter Notebook 使用Python内核，这就是为什么它原名 IPython Notebook。Jupyter notebook是Jupyter项目的产物——Jupyter这个名字是它要服务的三种语言的缩写：Julia，Python和R，这个名字与“木星（jupiter）”谐音。

2.快捷键：
高手们都知道，快捷键可以节省很多时间。Jupyter在顶部菜单提供了一个快捷键列表：Help > Keyboard Shortcuts 。每次更新Jupyter的时候，一定要看看这个列表，因为不断地有新的快捷键加进来。另外一个方法是使用Cmd + Shift + P ( Linux 和 Windows下 Ctrl + Shift + P亦可)调出命令面板。这个对话框可以让你通过名称来运行任何命令——当你不知道某个操作的快捷键，或者那个操作没有快捷键的时候尤其有用。这个功能与苹果电脑上的Spotlight搜索很像，一旦开始使用，你会欲罢不能。 
我比较常用的是：

Shift + M 合并cell. 可以选中cell后用来合并。
1~6 选中cell后用来设置6个级别的heading
L  可以用来切换显示或隐藏行号
H 用来调出快捷键操作指南
A 在选中的cell上方新加入一个cell
B 在选中的cell下方新加入一个cell
Y  将选中的cell转换为代码编辑模式
M 将选中的cell转换为Markdown模式
shift + enter 运行选中cell，并将光标挪到下一个cell
Ctrl + enter  运行选中cell，光标锁定到运行的cell
1
2
3
4
5
6
7
8
9
10
11
全部的快捷操作如下： 


3.全部显示
有一点已经众所周知。把变量名称或没有定义输出结果的语句放在cell的最后一行，无需print语句，Jupyter也会显示变量值。当使用Pandas DataFrames时这一点尤其有用，因为输出结果为整齐的表格。

鲜为人知的是，你可以通过修改内核选项ast_node_interactivity，使得Jupyter对独占一行的所有变量或者语句都自动显示，这样你就可以马上看到多个语句的运行结果了。

In [1]: from IPython.core.interactiveshell import InteractiveShell

        InteractiveShell.ast_node_interactivity = "all"
1
2
3
如果你想在各种情形下（Notebook和Console）Jupyter都同样处理，用下面的几行简单的命令创建文件~/.ipython/profile_default/ipython_config.py即可实现：

    c = get_config()

    # Run all nodes interactively

    c.InteractiveShell.ast_node_interactivity = "all"
1
2
3
4
5
6
7
这个刚了解时用起来很开心，不过当用到matplotlib时会输出很多信息，看起来比较丑，我就弃用了。

4.在notebook中作图
如果不想每次用matplotlib 作图后都要输入plt.show()来弹出显示图，可以如下：

matplotlib （事实标准）（http://matplotlib.org/），可通过%matplotlib inline 激活，（https://www.dataquest.io/blog/matplotlib-tutorial/） ===常用
%matplotlib notebook 提供交互性操作，但可能会有点慢，因为响应是在服务器端完成的。 ===需要调整图形时这个用着不错
mpld3（https://github.com/mpld3/mpld3） 提供matplotlib代码的替代性呈现（通过d3），虽然不完整，但很好。 ===没用过
bokeh（http://bokeh.pydata.org/en/latest/） 生成可交互图像的更好选择。 ====没用过
plot.ly（https://plot.ly/） 可以生成非常好的图，可惜是付费服务。===没用过
5.Jupyter notebook的magic操作
上面介绍的%matplotlib inline就是其中的一个魔术操作，作图时用起来流畅极了； 
%run ====用来运行代码脚本 
%store ====命令可以在两个notebook文件之间传递变量，没用过。。 
%who ====不加任何参数，命令可以列出所有的全局变量。加上参数 str 将只列出字符串型的全局变量

有两种用于计时的jupyter magic命令： 
当你有一些很耗时的代码，想要查清楚问题出在哪时，这两个命令非常给力。 
%%time 会告诉你cell内代码的单次运行时间信息。 
%%timeit 使用了Python的 timeit 模块，该模块运行某语句100，000次（默认值），然后提供最快的3次的平均值作为结果。 
%prun+函数声明会给你一个按顺序排列的表格，显示每个内部函数的耗时情况，每次调用函数的耗时情况，以及累计耗时。

Jupyter 有自己的调试界面The Python Debugger (pdb) 
===这个貌似很强大的样子，暂时还没用过，有机会我要试试~ 
（https://docs.python.org/3.5/library/pdb.html），使得进入函数内部检查错误成为可能。 
Pdb中可使用的命令见链接（https://docs.python.org/3.5/library/pdb.html#debugger-commands）

6.末句函数不输出
有时候不让末句的函数输出结果比较方便，比如在作图的时候，此时，只需在该函数末尾加上一个分号即可===这个用起来作的图看起来就清爽多了；

7.运行Shell命令
在notebook中可以用cd 来切换目录； 
ls用来显示当前目录内容； 
！pip install或者！conda install用来使用cmd下的命令操作；

8.支持多指针
Jupyter支持多个指针同步编辑，类似Sublime Text编辑器。按下Alt键并拖拽鼠标即可实现。====这个我用着很不顺手，按住ctrl后用移动鼠标可实现一样的多次选中，我还是喜欢用这个。。

9.Jupyter外界拓展
Jupyter-contrib extensions（https://github.com/ipython-contrib/jupyter_contrib_nbextensions）是一些给予Jupyter更多更能的延伸程序，包括jupyter spell-checker和code-formatter之类.

下面的命令安装这些延伸程序，同时也安装一个菜单形式的配置器，可以从Jupyter的主屏幕浏览和激活延伸程序。 
!pip install https://github.com/ipython-contrib/jupyter_contrib_nbextensions/tarball/master 
!pip install jupyter_nbextensions_configurator 
!jupyter contrib nbextension install –user 
!jupyter nbextensions_configurator enable –user 

这个用起来很爽，可以增加许多功能，尤其是里面可以增加侧边栏，这个用起来对代码管理就看起来层次分明多了，找代码也更方便了~~

10.隐藏代码只显示代码输出
from IPython.display import HTML

HTML('''<script>
code_show=true; 
function code_toggle() {
 if (code_show){
 $('div.input').hide();
 } else {
 $('div.input').show();
 }
 code_show = !code_show
} 
$( document ).ready(code_toggle);
</script>
<form action="javascript:code_toggle()"><input type="submit" value="Click here to toggle on/off the raw code."></form>''')
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
也可以这样：

code_show=true;
function code_toggle() {
 if (code_show){
 $('div.input').hide();
 } else {
 $('div.input').show();
 }
 code_show = !code_show
}

$([IPython.events]).on("app_initialized.NotebookApp", function () {
  $("#view_menu").append("<li id=\"toggle_toolbar\" title=\"Show/Hide code cells\"><a href=\"javascript:code_toggle()\">Toggle Code Cells</a></li>")
1
2
3
4
5
6
7
8
9
10
11
12
或者这样：

from IPython.display import display
from IPython.display import HTML
import IPython.core.display as di # Example: di.display_html('<h3>%s:</h3>' % str, raw=True)

# This line will hide code by default when the notebook is exported as HTML
di.display_html('<script>jQuery(function() {if (jQuery("body.notebook_app").length == 0) { jQuery(".input_area").toggle(); jQuery(".prompt").toggle();}});</script>', raw=True)

# This line will add a button to toggle visibility of code blocks, for use with the HTML export version
di.display_html('''<button onclick="jQuery('.input_area').toggle(); jQuery('.prompt').toggle();">Toggle code</button>''', raw=True)
1
2
3
4
5
6
7
8
9
这样：

$([IPython.events]).on('notebook_loaded.Notebook', function(){
    IPython.toolbar.add_buttons_group([
        {
             'label'   : 'toggle input cells',
             'icon'    : 'icon-refresh', 
             'callback': function(){$('.input').slideToggle()}
        }
    ]);
});
1
2
3
4
5
6
7
8
9
甚至可以这样：

# This is a cell to hide code snippets from displaying
# This must be at first cell!

from IPython.display import HTML

hide_me = ''
HTML('''<script>
code_show=true; 
function code_toggle() {
  if (code_show) {
    $('div.input').each(function(id) {
      el = $(this).find('.cm-variable:first');
      if (id == 0 || el.text() == 'hide_me') {
        $(this).hide();
      }
    });
    $('div.output_prompt').css('opacity', 0);
  } else {
    $('div.input').each(function(id) {
      $(this).show();
    });
    $('div.output_prompt').css('opacity', 1);
  }
  code_show = !code_show
} 
$( document ).ready(code_toggle);
</script>
<form action="javascript:code_toggle()"><input style="opacity:0" type="submit" value="Click here to toggle on/off the raw code."></form>''')

28
看自己爱好了，当然通过上面安装扩展的方式也自带了可以隐藏代码的方式~~ 
参考：http://stackoverflow.com/questions/27934885/how-to-hide-code-from-cells-in-ipython-notebook-visualized-with-nbviewer
