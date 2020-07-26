<h1>GDB调试</h1>


<h2>生成调试信息</h2>
使用gcc 加上-g选项

如果没有-g，将看不到函数名，变量名，所代替的全是运行时内存地址

gdb 运行程序<br>
准备调试程序

quit 退出调试代码

<ol>
<li>启动程序，可以按照你的自定义的要求随心所欲的运行程序</li>
<li>可以打断点(断点可以是条件表达式)</li>
<li>当程序被停住时，可以检查此时你的程序所发生的事</li>
<li>动态的改变你程序的执行环境</li>
</ol>


<h2>进入调试界面</h2>

<h3>设置运行参数</h3>
<ul>
<li>set args 运行参数 (set args 10 20 30 40 50)</li>
<li>show args 查看设置好的参数</li>
</ul>

<h3>启动程序</h3>
<ul>
<li>run 程序开始执行，如果有断点，停在第一个断点处</li>
<li>start 程序向下执行一行。(在第一条语句处停止)</li>
</ul>



<h2>查看源代码</h2>
list

<table>
<tr>
<th>命令选项</th>
<th>作用</th>
<th>命令选项</th>
<th>作用</th>
</tr>
<tr>


<tr>
<td>默认</td>
<td>显示当前运行处源代码</td>
<td>-</td>
<td>显示当前文件首行</td>
<tr>
<tr>
<td>linenum</td>
<td>打印第linenum行的上下文内容</td>
<td>function</td>
<td>显示函数名为function的函数源程序</td>
<tr>

<tr>
<td>file:linenum</td>
<td>显示file文件第linenum行</td>
<td>file:function</td>
<td>显示file文件下名为function的函数源代码</td>
<tr>


</table>


set listsize count  设置一次显示源代码的行数<br>
show listsize  查看当前设置行数


<h2>设置断点</h2>

break 设置断点，可以简写为b


info b 查看设置断点

next 执行一条语句

print argc 打印参数


b 10 设置断点，在源文件程序第10行<br>
b func 设置断点，在func函数入口处<br>
b file:func  设置断点，在file文件下func函数

disable 断点序列(2-4使2到4断点失效)  使断点无效<br>
enable 断点序列(1 3使断点1和3有效)  使断点有效

delete 断点序列  删除断点


<h2>条件断点</h2>

b 断点位置 if 条件表达式

如果条件表达式为真，才会是断点


<h2>调试代码</h2>

run 运行程序，可以简写为r<br>
next 单步调试，函数调用当作一条简单语句执行，可简写为n<br>
step 单步跟踪，进入被调用函数体内，可以简写为s<br>
finish 退出进入的函数，如果出不去，看下函数中的循环中是否有断点，如果有删掉或设置无效<br>
until 在一个循环体内单步跟踪时，这个命令可以运行直到退出循环，可简写为u，如果出不去，看下函数体中的循环中是否有断点，如果有删掉或这是无效<br>
continue 继续运行程序，可简写为c(若有断点则跳到下一个断点处)



<h2>查看变量值</h2>

print 变量值，变量地址

display 变量名称  自动显示变量值<br>
disable display 变量序号 设置变量无效<br>
enable display 变量序号  使变量有效<br>
delete display 变量序号  删除变量<br>


<h2>查看修改变量值</h2>
ptype 变量名称  打印变量类型


set var 变量=值 修改程序执行逻辑