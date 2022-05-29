####################[Install]###################
cp -a .vim ~/.vim  
cp -a .vimrc ~/.vimrc  

* Ctags:
cd ~/.vim/depends/  
unzip ctags-5.8.zip  
cd ctags-5.8  
./configure  
make  
sudo make install  

* vim 7.4.2367
wget https://github.com/vim/vim/archive/v7.4.2367.tar.gz  
tar zxvf v7.4.2367.tar.gz  
cd vim-7.4.2367/src/  
sudo make && sudo make install  

# Cscope:
参考Ctags步骤  
##################[快捷键定义]#################
* 1.窗口类:  
f2    鼠标使能切换  
\f2   行号显示切换  
f3    tagbarlist  
\f3   NERDTree  
f4    Ctrlp,文件模糊搜索,也可按ctrl+p打开,按esc退出  
\f4   MRU,文件打开历史记录,可保存  
f5    make tags,用于查看代码进入函数跳转,支持多目录加载  
\f5   make cscope,ctags的升级,功能更强大,暂不支持多目录加载  
f6    Buf exploler,当前文件打开记录缓存  
\f6   miniBufExploler,跟上一个类同  
\f7   themes switch  

* 2.文件跳转:  
1     跳转到上一个文件  
2     跳转到下一个文件  
\1    关闭当前文件  
3     quickfix列表搜索文件条状到下一个  
4     quickfix跳转到上一个  

* 3.更新插件:  
\3    更新插件  

* 4.退出:  
\q    退出当前窗口  
\qa   不保存seesion.vim退出全部  
\qs   保存session.vim退出全部  
F2    同\qs  
\w    :w  

* 5.ACK搜索相关:  
\s    Ack 搜索,先按下\s,再输入需要搜索的字符,回车  
\f    AckFile搜索,同上  

* 6.ag 搜索  
sudo apt-get install silversearcher-ag  

* 7.Cscope相关:  
cc  搜索该函数调用的函数  
cd  搜索调用该函数的函数  
cs  搜索函数  
cf  搜索文件  
ct  搜索字符串  

* 8.特殊命令:有时候vim的历史记录会有混乱，这个时候有两种方式还原:  
1> rm -rf ~./ctags/  
2> vim clean  
# #################[VIM 保存与恢复会话]#################
:mksession project.vim    创建并保存当前会话  
或  
:mksession! project.vim   保存当前会话并覆盖原会话  
:source    project.vim    恢复上次保存的会话  
vim -S project.vim        打开vim并恢复上次保存的会话  

# #################[VIM 挂起与恢复]#################
Ctrl-z    挂起vim程序  
{执行任何shell命令}  
fg        恢复vim程序  
'0        回到上次退出的位置，依次'1,'2...'9等  
:marks    显示出'0到'9的标记指向哪里  

# #################[VIM 执行shell命令]#################
* 格式:!{command}  
:!ls                   在vim中执行ls指令  
:!find ./ -name "*.c"  在vim中执行find指令  
:!xterm&               从vim中新打开xterm  
:shell                 从vim中打开新shell  

# #################[VIM 窗口操作]#################
* 1.new 命令  
:new name 新建一个名为name的窗口  

* 2.split命令  
:split/sp name 在当前位置打开name窗口 将原来文件向下移动(sp是split的缩写)  

* 3.vsplit命令  
:vsplit/vs name 在当前位置打开name文件 将原来文件向右移动(vs是vsplit的缩写)  

* 4.快捷键分屏  
Ctrl+W s 水平分割当前打开的文件，相当于执行split省略文件名的命令  
Ctrl+W v 垂直分割当前打开的文件，相当于执行vsplit省略文件名的命令  

* 5.分屏启动Vim  
vim -on/-On file1 file2 …   大写的O表示垂直分屏 / 小写的o表示水平分屏 / n是数字，表示分成几个屏  

* 6.多窗口移动  
ctrl + h/j/k/l  移动到左/下/上/右窗口  

* 7.关闭多窗口  
:qall    退出所有窗口，如果修改未保存需要手动":w/:q"保存/退出  
:qall!   不保存退出当所有窗口  
:wall    保存退出当所有窗口  

# #################[VIM 移动和跳转操作]#################
''       跳转到上次光标停留位置，两点来回跳转  
Ctrl+o   跳转到上次光标停留位置，基于当前状态一直往前跳  
Ctrl+i   跳回到Ctrl+o 跳过的位置  
g;       光标跳转到前一次修改位置  
g,       光标跳转到后一次修改位置  
%        括号匹配(),[],{},#if...#else..#endif  
[[       向下跳转到函数"{"  
]]       向上跳转到函数"{"  

# #################[ctags 指令]#################
* 1.生产ctags的索引文件:tags  
cd /data/proj               进入代码目录  
ctags -R .                  搜索整个代码目录并生成tags文件  
:set tags=/data/proj/tags   在vim中引用tags文件，方便函数间跳转  

* 2.常用ctags命令
Ctrl+]       跳转至光标出函数、变量、宏等定义的地方  
Ctrl+t       回调到上次跳转的函数、变量、宏位置   
:tags        显示你到过的tag列表，即跳转栈信息  
:tag         跳转到tag栈的下一个  
:Ntag        以步进N在tag栈中跳转，例如:3tag 表示在栈中连跳三个tag  
:tag  name   跳转到name定义的地方和"Ctrl+]"功能类似  
:stag name   分割窗口中显示name定义，光标停留在新窗口，使用":close"关闭分割窗口  
:ptag name   预览窗口中显示name定义，光标停留在新窗口，使用":pclose"关闭预览窗口  
 
# #################[cscope 指令]#################
* 1.生产cscope的索引文件:cscope.out  
cd /data/proj             进入代码目录  
cscope -Rbkq              R:表示把所有子目录里的文件也建立索引  
                          b:表示cscope不启动自带的用户界面，而仅仅建立符号数据库  
                          q:生成cscope.in.out和cscope.po.out文件，加快cscope的索引速度  
                          k:在生成索引文件时，不搜索/usr/include目录  
:cs add ./cscope.out      在vim中加载索引库，方便函数间跳转  

* 2.常用的cscope命令  
：cs find s               查找C语言符号，即查找函数名、宏、枚举值等出现的地方  
：cs find g               查找函数、宏、枚举等定义的位置，类似ctags所提供的功能  
：cs find d               查找本函数调用的函数  
：cs find c               查找调用本函数的函数  
：cs find t:              查找指定的字符串  
：cs find e               查找egrep模式，相当于egrep功能，但查找速度快多了  
：cs find f               查找并打开文件，类似vim的find功能  
：cs find i               查找包含本文件的文件  

# ############[ push code to github ]#####################
* Push:  
* You can do :  

git add .;  
git commit -am "<xxx>";  
git remote add origin https://github.com/Jiawang-Ding/vim-warper  
git pull origin master;  
git push -u origin master;  

* Download:  
git clone https://github.com/Jiawang-Ding/vim-warper  

* Update:  
git pull origin master;  

