# CentonOS Vim7.2.411 编辑器的配置


<br>

#### 效果预览 <br>
![fanal](https://github.com/xiyelin/Linux/tree/master/picture/fanal.png)

<br>
#####0.安装Vim：<br>

    　　如果你的Linux系统中还没有安装Vim可以去官网下载：http://www.vim.org ，或者直接使用命令：yum -y install vim 进行安装。


<br>
##### 1.设置路径<br>
    　　查看你的 /home/ 目录下有没有 .vim 和 .vimrc 这两个文件，因为是隐藏文件，所以查看时要用 ls -a 命令，如果没有就新建这两
    
    个目录。你可能会发现在你的 /etc/ 下面这两个文件已经存在了，没关系；/etc 目录下时针对所有用户的 Vim 配置，而 /home/ 只针对
    
    当前用户。 (注意 .vim 是目录， .vimrc 是配置文件)
    
    　　并且在 .vim 路径下创建下面三个目录：
    　　
    　　~/.vim/doc
    　　~/.vim/plugin
    　　~/.vim/syntax
    
<br>  
##### 2.Vim中文帮助手册下载<br>

    　　下载地址： https://sourceforge.net/
    　　
    　　将文件解压后的 doc 文件的内容复制到 ~/.vim/doc 下。这时你的 Vim 帮助文档就是中文的了。
    
    　　如果无法显示中文： 在 ~/.vimrc 添加： set helplang=cn
    　　
    　　如果想在 Vim 中直接查看，在 ~/.vimrc 添加：set encoding=utf-8
    　　
    　　现在你打开 Vim 在底行模式下输入命令：help 就可以查看中文帮助文档了。
    　　
<br>
![fanal](https://github.com/xiyelin/Linux/tree/master/picture/help.png)
<br>
![fanal](https://github.com/xiyelin/Linux/tree/master/picture/helppage.png)
<br>

##### 3.配置 .vimrc <br>

    set nu                     "显示行号 
    syntax enable 
    syntax on                  "语法高亮 
    set tabstop=4              "tab键默认4个空格 
    set history=500            "历史记录500条 
    set ruler                  "打开状态栏坐标消息 
    set laststatus=1           "取消底部栏显示，1为开启，2为关闭 
    set showcmd                "将输入的命令显示出来 
    set cursorline             "下划线高亮显示所在行 
    set showmatch              "插入右括号时会短暂的跳转到匹配的左括号 
    let loaded_matchparen=1    "不对匹配的括号进行高亮显示 
    set softtabstop=4          "按退格键时，如果前面有4个空格，则退回4个空格 
    set cindent shiftwidth=4   "换行自动缩进 
    set expandtab              "高亮显示搜索匹配到的字符串 
    set nobackup               "取消备份 
    set noswapfile             "禁止临时文件的产生 
    set autoindent             "设置自动对齐(缩进):即每行的缩进值与上一行相等
    set cindent                "设置C/C++自动对齐 
    set t_Co=256               "指定配色方案为256 
    set ignorecase             "搜索时忽略大小写 
    set mouse=a                "在vim中可以使用鼠标 
    colorscheme desert         "配色方案 
    filetype plugin on         "允许插件

<br>
##### 3.安装 Ctags 插件 <br>

    　　Ctags 的作用：为源码的变量/对象、结构体/类、函数/接口、宏等产生索引文件，以便快速定位。 安装： yum -y install ctags 
    　　
    　　使用方法：
    　　
    　　      使用命令ctags -R 将在源码目录下生成一个tags文件。
    　　    
    　　      tags文件是由ctags程序产生的一个索引文件, 如果你在读程序时看了一个函数调用, 或者一个变量, 或者一个宏等等, 你想
    
        知道它们的定义在哪儿, 怎么办呢? 用grep? 那会搜出很多不相干的地方. 现在可以用<C-]>,即 Ctrl + ] 。查看完之后如果想回
        
        到跳转之前的地方，则使用命令 <C - T>，即 Ctrl + T 即可。(可以使用 :help usr_29 在Vim帮助手册中查看详细的使用教程)

<br>
![fanal](https://github.com/xiyelin/Linux/tree/master/picture/ctags.png)
<br>
##### 4.安装 Taglist 插件 <br>

    　　插件作用：在Vim窗口中显示当前文件中所有宏，全局变量和函数等内容，方法查看。
    　　
    　　下载地址：http://www.vim.org/scripts/script.php?script_id=273
    　　
    　　安装方法：将文件解压到 ~/.vim/ 路径下，可以将对应的 doc 和 plugin 文件内容统一放在之前建好的 doc 和 plugin 文件中。
    　　
    　　帮助手册，同样在 Vim 底行模式输入命令： help taglist.txt 即可查看帮助文档。
    　　
    　　除此之外，要想使用 TagList 插件必须还要配置一下 .vimrc 文件，配置内容如下：
    　　
    　　      let Tlist_Show_One_File = 1        "只显示当前文件的tag
    　　      let Tlist_Exit_OnlyWindow = 1      "如果taglist是最后一个窗口，则退出 Vim
    　　      
    　　启动 Vim 之后，使用底行模式输入：Tlist 即可进入该界面。

<br>
![fanal](https://github.com/xiyelin/Linux/tree/master/picture/TagList.png)
<br>
##### 5.安装  WinManager 插件 <br>

    　　下载地址： http://www.vim.org/scripts/script.php?script_id=95
    　　
    　　安装方法：将压缩包解压到 ~/.vim/ 目录下。
    　　
    　　帮助手册：help winmanager
    　　
    　　插件动能：将当前目录下的所有目录和文件显示出来，可以像图形化界面一样操作文件和目录。
    　　
    　　配置 ~/.vimrc ：
    　　
        let g:winManagerWindowLayout = "BufExplorer,FileExplorer|TagList"
        
        let g:winManagerWindowLayout = "TagList|FileExplorer,BufExplorer"   "设置分割线，选择一个即可
    　　
    　　nmap wm :WMToggle<cr>               "winmanager快捷键 
        
        let g:AutoOpenWinManager = 1        "自动打开winmanager界面 
        
        let g:winManagerWidth = 30          "设置宽度为30，默认为25 
        
        打开方式：
        
                在 Vim 命令模式下直接输入 wm 即可进入该界面。

<br>
![fanal](https://github.com/xiyelin/Linux/tree/master/picture/WinManager.png)
<br>
##### 6.安装 MiniBufExplorer 插件 <br>

    　　下载地址：http://www.vim.org/scripts/script.php?script_id=159
    　　
    　　安装方法：将下载的文件放到 ~/.vim/plugin 文件中。
    　　
    　　插件功能：在 Vim 最上边一行显示所有打开的文件，是一个缓冲区。
    　　
    　　配置 .vimrc ：
    　　
    　　    let g:minBufExplMapCTabSwitchBufs = 1    "Tab和S-Tab键切换
    　　    
    　　
    　　快捷键：
    　　        
    　　        <Tab> 向前循环切换          <S-Tab>向后循环切换
    　　      
    　　        <Enter> 打开光标所在的文件       d  删除光标所在的文件
    　　        

<br>
![fanal](https://github.com/xiyelin/Linux/tree/master/picture/miniBuffer.png)
<br>

##### 7.安装 A 插件 <br>

    　　下载地址：http://www.vim.org/scripts/script.php?script_id=31
    　　
    　　安装方法：将 a.vim 文件放到 ~/.vim/plugin/ 下面。
    　　
    　　插件功能：进行头文件和源文件之间的切换
    　　
    　　配置 .vimrc ：
    　　    
    　　        nnoremap<silent><F12>:A<CR>     "按F12在一个新的buffer中打开c/h文件   
    　　        
    　　快捷键：
    　　
    　　        A  在新缓冲区中切换到c/h文件
    　　        AS 横向分割窗口并打开c/h文件
    　　        AV 纵向分割窗口并打开c/h文件
    　　        AT 新建一个标签页并打开c/h文件
    　　        










