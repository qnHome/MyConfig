# myVim
我的Vim配置

## 安装
(使用python编译vim环境. 检查命令 `vim --version | grep +python`)

* **依赖**(Debian/Ubuntu)

    `sudo apt-get install python vim exuberant-ctags git`

    `sudo pip install pep8 flake8 pyflakes isort`

* **依赖**(RedHat/CentOS)

    The CentOS 6.7's default Python is 2.6, it's recommend to install Python2.7.

    `sudo yum install python vim ctags git`

    `sudo pip install pep8 flake8 pyflakes isort`

* **依赖**(Mac OS platform)

    `brew install python vim git`

    `wget --no-check-certificate http://tenet.dl.sourceforge.net/project/ctags/ctags/5.8/ctags-5.8.tar.gz && tar -zxvf ctags-5.8.tar.gz && cd ctags-5.8 && ./configure && make && sudo make install`

    `sudo pip install pep8 flake8 pyflakes isort`

* **下载 .vimrc 文件到 /home/user 目录**

    `wget --no-check-certificate https://raw.githubusercontent.com/qnHome/vim/master/vimrc -O $HOME/.vimrc`

* **打开Vim**

    Open vim, it will install plugins automatically. Wait for the installation to be finished.
    Or you can run

    `vim -E -u $HOME/.vimrc +qall`

* **完成，开始享受吧~**

## 特征

### 插件管理(Vundle)

使用[**Vundle**](https://github.com/VundleVim/Vundle.vim)作为插件管理器，Vundle会自动管理`.vim` 文件夹下所有的插件，插件会默认被下载到`~/.vim/bundle/`中，请保持 `.vim` 文件夹在使用前已经clean。当Vundle安装插件时会触发 `git clone`操作，搜寻操作需要`curl`。

#### 配置(举例一部分)

```vim
" let Vundle manage Vundle
Plugin 'gmarik/vundle'

" ============================================================================
" Active plugins
" You can disable or add new ones here:

" Plugins from github repos:

" Better file browser
Plugin 'scrooloose/nerdtree'
" Code commenter
Plugin 'scrooloose/nerdcommenter'
" Class/module browser
Plugin 'majutsushi/tagbar'
" Code and files fuzzy finder
Plugin 'kien/ctrlp.vim'
" Extension to ctrlp, for fuzzy command finder
Plugin 'fisadev/vim-ctrlp-cmdpalette'
" Zen coding
Plugin 'mattn/emmet-vim'
" Git integration
Plugin 'motemen/git-vim'
" Tab list panel
Plugin 'kien/tabman.vim'

```

#### 支持的操作

|   命令             |    描述        |
|-----------------------|:---------------------:|
|  :PluginList          |   列出插件列表    |
|  :PluginInstall(!)    | 安装/更新插件 |
|  :PluginSearch(!) foo | foo插件搜索 |
|  :PluginClean(!)      |  清除无用插件 |
|  :PluginUpdate        |      更新插件   |


### 项目文件浏览器（NERDTree）

在vim配置中我使用了[**NERDTree**](https://github.com/scrooloose/nerdtree) 作为文件浏览器。NERDTree允许开发者浏览你的文件系统，并且可打开相应的文件和文件夹。他也允许你隐藏文件或设置书签等等。在NERDTree窗口输入`?`可以获取操作引导。这个配置中设置会过滤掉 `.pyc`, `.git`, `.hg`, `.svn`等。

#### 配置

```vim
" auto open or close NERDTree
autocmd vimenter * if !argc() | NERDTree | endif
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") && b:NERDTreeType == "primary") | q | endif

" NERDTree -----------------------------

" toggle nerdtree display
map <F3> :NERDTreeToggle<CR>
" open nerdtree with the current file selected
nmap ,t :NERDTreeFind<CR>
" don;t show these file types
let NERDTreeIgnore = ['\.pyc$', '\.pyo$']
```

#### 所支持的操作

| 快捷键         |    描述             |
|-----------------------|:--------------------------:|
|      F3               | 打开/关闭 NERDTree        |
|      ,t               |打开 NERDTree 并选择当前文件|


### 语法检查

在vim的配置中，我使用了 [**Syntastic**](https://github.com/scrooloose/syntastic) 插件用来做语法检查，支持`C/C++/Go/Python/Haskell/Ruby/JavaScript`等。对于JavaScript，我使用`eslint`作为检查器，所以它能够检查 ES6 和 JSX 等.
你可以查看[JSLint, JSHint和ESLint的对比及Vim配置](http://moelove.info/2015/11/28/JSLint-JSHint-ESLint%E5%AF%B9%E6%AF%94%E5%92%8CVim%E9%85%8D%E7%BD%AE/)的更多细节，如果你想更换检查器的话，仅需要很简单的配置。


#### 配置

```vim
" Syntastic ------------------------------

" show list of errors and warnings on the current file
nmap <leader>e :Errors<CR>
" turn to next or previous errors, after open errors list
nmap <leader>n :lnext<CR>
nmap <leader>p :lprevious<CR>
" check also when just opened the file
let g:syntastic_check_on_open = 1
" syntastic checker for javascript.
" eslint is the only tool support JSX.
" If you don't need write JSX, you can use jshint.
" And eslint is slow, but not a hindrance
" let g:syntastic_javascript_checkers = ['jshint']
let g:syntastic_javascript_checkers = ['eslint']
" don't put icons on the sign column (it hides the vcs status icons of signify)
let g:syntastic_enable_signs = 0
" custom icons (enable them if you use a patched font, and enable the previous 
" setting)
let g:syntastic_error_symbol = '✗'
let g:syntastic_warning_symbol = '⚠'
let g:syntastic_style_error_symbol = '✗'
let g:syntastic_style_warning_symbol = '⚠'
```

#### 特征

When you save files, it will check syntax automatically, and display syntax errors.

#### 支持的操纵

|   shortcut key        |    description             |
|-----------------------|:--------------------------:|
|       `\e`            |     列出语法错误     |
|       `\n`            |     转到下一个错误     |
|       `\p`            |     转到上一个错误 |
