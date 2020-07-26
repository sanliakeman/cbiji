<h1>预处理阶段</h1>

<b>
	<font color="green">gcc</font>
</b> -E sourceFilename.c -o targetFilename.i

工作内容
<ul>
	<li>加载include文件内容</li>
	<li>初始化define值</li>
	<li>删除注释</li>
	<li>展开条件编译</li>
</ul>


<h1>编译阶段</h1>


<b>
	<font color="green">gcc</font>
</b> -S sourceFilename.i -o targetFilename.s

工作内容
<ul>
	<li>逐行检查语法错误<font color="red">(是最耗时的过程)</font></li>
	<li>翻译成汇编指令</li>
</ul>

<h1>汇编阶段</h1>

<b>
	<font color="green">gcc</font>
</b> -c sourceFilename.s -o targetFilename.o

查看二进制文件
	<font color="green">hex</font> filename.o

工作内容
<ul>
	<li>转换为二进制文件</li>
</ul>


<h1>链接阶段</h1>

<b>
	<font color="green">gcc</font>
</b>  sourceFilename.o -o targetFilename


工作内容
<ul>
	<li>数据段合并</li>
	<li>数据地址回填</li>
	<li>库引入</li>
	<li>变成可执行文件</li>
</ul>





<h2>常用参数</h2>
<table>
<tr>
<th>快捷键</th>
<th>作用</th>
<th>快捷键</th>
<th>作用</th>
</tr>
<tr>


<tr>
<td>-I</td>
<td>指定头文件所在位置</td>
<td>-L</td>
<td>指定库文件所在位置</td>
<tr>
<tr>
<td>-l</td>
<td>指定库的名字</td>
<td>-o</td>
<td>指定生成目标文件的名字</td>
<tr>

<tr>
<td>-g</td>
<td>包含调试信息</td>
<td>-On</td>
<td>n=0~3 编译优化,n越大优化的越多</td>
<tr>


</table>



<h2>库文件</h2>

<h3>静态库</h3>

目标代码的集合，是在可执行程序运行前已经加入到执行代码中，成为程序一部分。一般以.a文件名后缀

静态库的命名一般分为三个部分
<ul>
<li>前缀: lib</li>
<li>库名称: 可以自定义 </li>
<li>后缀: .a</li>
</ul>
链接静态库使用<br>
gcc -o main main.c -I./ -L./ -lxxx

步骤:

<ol>
<li>将源文件生成.o文件</li>
<li>使用打包工具ar将准备好的.o文件打包成为.a文件
ar rcs libxxx.a fun1.o fun2.o
</li>
</ol>


<h3>动态库</h3>

共享库在程序编译时不会链接到目标代码中,而是在程序运行时才会载入


动态库的命名一般分为三个部分
<ul>
<li>前缀: lib</li>
<li>库名称: 可以自定义 </li>
<li>后缀: .so</li>
</ul>
gcc -o main main.c -I./ -L./ -lxxx

步骤:

<ol>
<li>生成目标文件.o,此时要加选项:fPIC
gcc -fpic -c fun1.c fun2.c
参数: -fpic创建与地址无关的编译程序,目的就是为了能够在多个应用程序间共享
</li>
<li>生成共享库,此时要加链接器选项:-shared(指定生成动态链接库)
gcc -shared fun1.o fun2.o -o libxxx.so
</li>
</ol>

file 文件名<br>
查看文件格式


ldd 可执行文件

ldd命令可以查看执行文件依赖的库文件

对于elf格式可执行文件,是由ld-linux.so*来完成的,它先后搜索elf文件的DT_RPATH段-环境变量LD_LIBARY_PATH-/etc/ld.so.cache文件列表-
/lib/,/usr/lib目录找到库文件后将其载入内存


临时设置LD_LIBARY_PATH<br>
export LD_LIBARY_PATH=$LD_LIBARY_PATH:库路径

永久设置

~/.bashrc文件
加上路径

export LD_LIBARY_PATH=$LD_LIBARY_PATH:库路径

使文件生效
<ul>
<li>. ~/.bashrc</li>
<li>或source ~/.bashrc</li>
</ul>