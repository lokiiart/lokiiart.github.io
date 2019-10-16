---
title: 对vim的执念
date: 2019-09-17 03:02:26
tags: Linux
---

撸Linux不撸vim，
撸破minix也枉然。

<!--more-->

Vim是我接触的第一个编辑器，哦，不，之前还用过notepad++，在我还不知道代码是什么的时候。
然后，这些年一直没有好好地用起来，除了hjkl，就只会一些最基本的操作，也没有离不开的插件之类的。
究其原因，最开始用的时候，实在是被网上那些洗脑的文章毒害得不清，就只想把该装的都装上，好好装逼，其实那时候就写写谭浩强C，配置配置Ubuntu，那时候的插件安装配置也没有现在这么简单，有没有真实的需求，自然是心力憔悴又不讨好。

虽然当年没有用好，但是vim最精华的hjkl还是用熟了。于是，Eclipse/VS/JetBrains系列到后来的VSCODE，都一律vim按键映射。遇见vscode的时候，我一度以为再也不会回到vim了。vscode很简单的傻瓜配置就能够拥有堪比IDE的功能，并且，全平台，更轻量，更好看，按键也很统一，夫复何求啊。
当然它也慢慢在我手里变得臃肿了，我其实没做什么，后来我都分开做了，不想着一个工具解决所有问题，后端C#在VS上面写，前端才用vscode，但是它还是变胖了，可能是项目代码越来越大了吧，打开程序慢悠悠的，打开文件慢悠悠的。后来我也不在编辑器里面跑服务了，也不在里面debug了，KISS原则嘛。
但是就是越来越不爽了。


后来，恰巧那几天对LISP感兴趣，想着ELISP不就是最方便成熟的环境么，随便写点什么练练手吧，下了个EMACS，用了五分钟，这奇葩的快捷键，怎么能和我大vim比，顺手搜了一下vim的新闻，这货最近闹得很欢腾啊。哦，对vim来说，两三年应该是很短的时间吧。
这心头之好当然得下下来体验一下。随便折腾了一下，没什么变化啊，还是老样子啊。

直到，我遇见了一个大文件，也没多大，1M左右而已，在vscode里面卡得呦。鬼使神差地用vim试了一下，那流畅度，跟打开helloworld没有区别啊。

卧槽，终于找到理由再次折腾vim了，欢天喜地项目也扔到一边，劈里啪啦一顿整。
于是，终于完成了下面配置。

我最近大爱windows，windows
termial/wsl都在用。所以是gvim，然后，我想说的是，vscode的卡顿是整个家族的问题，terminal下用vim打开的文件稍微大一点也卡得一逼。gvim应该是用的win32，会好一些，但是打开还是会卡一会儿。

然后，在gnome下用gvim完全不存在卡顿的问题，如丝绸般顺滑。

看了那么多把vim当IDE来用的文章，终于我也可以装装逼了。

真的建议新手不要像我一样，上来就用vim，你不清楚自己的需求，vim配不上你纯真的想象。最好是用用现代的编辑器或者IDE，等你习惯了那些便捷功能之后，再来把vim配成你想要的样子。这个时候vim才是那个365面，你想要的样子我都有的编辑器之神。

    cd ~\OneDrive\Documents\GitHub
    "editor config
    set encoding=utf-8
    set fileencoding=utf-8
    set fileencodings=utf-8
    let $LANG = 'en_US.UTF-8'
    set nocompatible
    set showmode
    set showcmd
    "set autochdir
    set noerrorbells
    set visualbell
    set autoread
    set mouse=a
    set t_Co=256
    set number
    set relativenumber
    set splitbelow
    set splitright
    set cursorline
    set noshowmode

    if has("gui_running")
        "au GUIEnter* simalt ~x
        set guioptions-=m
        set guioptions-=T
        set guioptions-=e
        set guioptions-=r
        set guioptions-=R
        set guioptions-=L
        set guioptions-=l
        "正经字体
        set guifontwide=Sarasa_Mono_CL:h14:cCHINESEBIG5:qDRAFT
        set guifont=SauceCodePro_NF:h14:cANSI:qDRAFT
        "好玩字体
        "set guifont=Anonymice_NF:h14:cANSI:qDRAFT
        "set guifont=3270Medium_NF:h16:W500:cANSI:qDRAFT
        "set guifont=mononoki_NF:h14:cANSI:qDRAFT
    endif


    set textwidth=80
    set nowrap
    set scrolloff=5
    set sidescrolloff=15

    set listchars=tab:»■,trail:■
    set list
    set wildmenu
    set wildmode=longest:list,full

    set showtabline=2
    set laststatus=2
    set ruler

    "search config
    set showmatch
    set incsearch
    set ignorecase
    set smartcase

    "edit config
    filetype on
    syntax on
    filetype indent on
    filetype plugin on

    set smartindent
    set tabstop=2
    set shiftwidth=2
    set expandtab
    set softtabstop=2

    "file config
    set nobackup
    set nowritebackup
    set noswapfile

    set cmdheight=2

    set pyxversion=3
    let &pythonthreedll='C:\Python37\python37.dll'
    let &pythonthreehome='C:\Python37'
    let g:pymode_python='python3'
    let g:python3_host_prog=expand('C:\Python37\python.exe')
    "let g:python3='C:\Python37\python.exe'


    "=====Set mapleader====
    let mapleader = ","

    "Fast reloading of the .vimrc
    map <silent> <leader>ss :source ~/_vimrc<cr>
    "Fast editing of .vimrc
    map <silent> <leader>ee :e ~/_vimrc<cr>
    "When .vimrc is edited, reload it
    autocmd! bufwritepost _vimrc source ~/_vimrc

    noremap <silent><c-s> :w<CR>





    call plug#begin()
    "====General====
    "基础设施nvim通信
    Plug 'roxma/nvim-yarp'
    Plug 'roxma/vim-hug-neovim-rpc'

    "Git
    Plug 'tpope/vim-fugitive'
    "Plug 'airblade/vim-gitgutter'

    "colorscheme
    Plug 'morhetz/gruvbox'
    Plug 'ayu-theme/ayu-vim' "
    Plug 'dracula/vim', { 'as': 'dracula' }
    Plug 'taigacute/gruvbox9'
    Plug 'joshdick/onedark.vim'

    "美化
    Plug 'itchyny/lightline.vim'
    Plug 'niklaas/lightline-gitdiff'
    Plug 'mengelbrecht/lightline-bufferline'



    Plug 'ryanoasis/vim-devicons'

    "行为习惯
    Plug 'tpope/vim-sensible'
    Plug 'yuttie/comfortable-motion.vim'
    Plug 'Raimondi/delimitMate' "自动补全括号


    "扩展工具
    Plug 'jlanzarotta/bufexplorer' "remember the shortcort '<leader>bv'
    Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' },
    Plug 'Xuyuanp/nerdtree-git-plugin'
    Plug 'Yggdroot/LeaderF', { 'do': '.\install.bat' }

    "缩进对齐
    Plug 'yggdroot/indentline'
    Plug 'junegunn/vim-easy-align'


    "奇技淫巧
    Plug 'tpope/vim-surround', "两边添加，还没用习惯
    Plug 'tpope/vim-repeat' "搭配使用，口感更佳
    Plug 'easymotion/vim-easymotion' "大名鼎鼎


    "====Language====
    "General
    Plug 'sheerun/vim-polyglot' "高亮

    Plug 'scrooloose/nerdcommenter', "注释

    "javascript
    Plug 'pangloss/vim-javascript',  {'for': ['html', 'css', 'js', 'javascript', 'javascript.jsx', 'jsx']} "javascript
    Plug 'chemzqm/vim-jsx-improve',  {'for': ['html', 'css', 'js', 'javascript', 'javascript.jsx', 'jsx']}

    "ml&&jsx&&html
    Plug 'docunext/closetag.vim'      "html close the tag
    "Plug 'mxw/vim-jsx',    {'for': ['jsx', 'javascript.jsx']}            "jsx s
    Plug 'vim-scripts/matchit.zip',    "html标签配对跳转，vim-sensible配的不行
    "Plug 'mattn/emmet-vim', {'for': ['html', 'css']}             "html-snippet

    "AutoComplete
    Plug 'neoclide/coc.nvim', {'branch': 'release'}

    Plug 'Shougo/neosnippet.vim'
    Plug 'Shougo/neosnippet-snippets'

    call plug#end()

    "====set tab&buffer switch====
    if has('gui_running') 
      set winaltkeys=no
      "set macmeta
      noremap <silent><c-tab> :bn<CR>
      inoremap <silent><c-tab> <ESC>:bn<CR>
      noremap <silent><c-s-tab> :bp<CR>
      inoremap <silent><c-s-tab> <ESC>:bp<CR>
      noremap <silent><m-t> :tabnew<CR>
      inoremap <silent><m-t> <ESC>:tabnew<CR>
      noremap <silent><m-w> :tabnew<CR>
      inoremap <silent><m-w> <ESC>:tabnew<CR>
      noremap <silent><m-1> :tabn 1<cr>
      noremap <silent><m-2> :tabn 2<cr>
      noremap <silent><m-3> :tabn 3<cr>
      noremap <silent><m-4> :tabn 4<cr>
      noremap <silent><m-5> :tabn 5<cr>
      noremap <silent><m-6> :tabn 6<cr>
      noremap <silent><m-7> :tabn 7<cr>
      noremap <silent><m-8> :tabn 8<cr>
      noremap <silent><m-9> :tabn 9<cr>
      noremap <silent><m-0> :tabn 10<cr>
      inoremap <silent><m-1> <ESC>:tabn 1<cr>
      inoremap <silent><m-2> <ESC>:tabn 2<cr>
      inoremap <silent><m-3> <ESC>:tabn 3<cr>
      inoremap <silent><m-4> <ESC>:tabn 4<cr>
      inoremap <silent><m-5> <ESC>:tabn 5<cr>
      inoremap <silent><m-6> <ESC>:tabn 6<cr>
      inoremap <silent><m-7> <ESC>:tabn 7<cr>
      inoremap <silent><m-8> <ESC>:tabn 8<cr>
      inoremap <silent><m-9> <ESC>:tabn 9<cr>
      inoremap <silent><m-0> <ESC>:tabn 10<cr>
      nmap <Leader>1 <Plug>lightline#bufferline#go(1)
      nmap <Leader>2 <Plug>lightline#bufferline#go(2)
      nmap <Leader>3 <Plug>lightline#bufferline#go(3)
      nmap <Leader>4 <Plug>lightline#bufferline#go(4)
      nmap <Leader>5 <Plug>lightline#bufferline#go(5)
      nmap <Leader>6 <Plug>lightline#bufferline#go(6)
      nmap <Leader>7 <Plug>lightline#bufferline#go(7)
      nmap <Leader>8 <Plug>lightline#bufferline#go(8)
      nmap <Leader>9 <Plug>lightline#bufferline#go(9)
      nmap <Leader>0 <Plug>lightline#bufferline#go(10)
    endif

    function! StatusDiagnostic() abort
      let info = get(b:, 'coc_diagnostic_info', {})
      if empty(info) | return ' ' | endif
      let msgs = []
      if get(info, 'error', 0)
        call add(msgs, '' . info['error'])
      endif
      if get(info, 'warning', 0)
        call add(msgs, '⚠' . info['warning'])
      endif
      if get(info, 'information', 0)
        call add(msgs, '' . info['information'])
      endif
      if get(info, 'hint', 0)
        call add(msgs, 'H' . info['hint'])
      endif
      return join(msgs, ' '). '' . get(g:, 'coc_status', '') 
    endfunction

    function! LightLineFileName()
      return expand('%:.')
    endfunction

    let g:lightline = {
          \ 'colorscheme': 'gruvbox9',
          \ 'active': {
          \   'left': [ [ 'mode', 'paste' ],
          \             ['gitbranch', 'gitdiff', 'readonly', 'filename', 'modified']],
          \   'right': [[ 'lineinfo' ],
          \              [ 'percent' ],
          \              [ 'fileformat', 'fileencoding', 'filetype' ],
          \              [ 'currentfunction' ]]
          \ },
          \ 'component_function': {
          \   'gitbranch': 'fugitive#head',
          \   'filename': 'LightLineFileName',
          \   'gitdiff': 'lightline#gitdiff#get',
          \   'cocstatus': 'coc#status',
          \   'currentfunction': 'StatusDiagnostic'
          \ },
          "\ 'component_expand': {
          "\   'gitdiff': 'lightline#gitdiff#get',
          "\ },
          "\ 'component_type': {
          "\   'gitdiff': 'middle',
          "\ },
          \ 'separator': { 'left': '', 'right': '' },
          \ 'subseparator': { 'left': '', 'right': '' }
          \ }

    let g:lightline#bufferline#filename_modifier = ':t'
    let g:lightline#bufferline#show_number  = 2
    let g:lightline#bufferline#shorten_path = 0
    let g:lightline#bufferline#unicode_symbols = 1
    let g:lightline#bufferline#enable_devicons = 1
    let g:lightline#bufferline#number_map = {
    \ 0: '⁰', 1: '¹', 2: '²', 3: '³', 4: '⁴',
    \ 5: '⁵', 6: '⁶', 7: '⁷', 8: '⁸', 9: '⁹'}
    let g:lightline.tabline          = {'left': [['buffers']], 'right': [['tabs']]}
    let g:lightline.component_expand = {'buffers': 'lightline#bufferline#buffers'}
    let g:lightline.component_type   = {'buffers': 'tabsel'}

    let g:comfortable_motion_no_default_key_mappings = 1
    nnoremap <silent> <C-d> :call comfortable_motion#flick(180)<CR>
    nnoremap <silent> <C-u> :call comfortable_motion#flick(-180)<CR>
    let g:comfortable_motion_interval = 1000.0/120
    let g:comfortable_motion_friction = 140.0
    let g:comfortable_motion_air_drag = 4.0


    let NERDTreeShowHidden=1
    let NERDTreeWinSize=35
    let g:NERDTreeDirArrowExpandable = '▸'
    let g:NERDTreeDirArrowCollapsible = '▼'

    noremap <silent><c-e> :NERDTreeToggle<cr>
    inoremap <silent><c-e> <ESC>:NERDTreeToggle<cr>
    nnoremap <silent> <c-l>  :<C-u>LeaderfLine<cr>
    nnoremap <silent> <c-m>  :<C-u>LeaderfMru<cr>
    let g:Lf_ShortcutF = '<c-f>'
    let g:Lf_ShortcutB = '<C-b>'


    xmap ga <Plug>(EasyAlign)
    nmap ga <Plug>(EasyAlign)



    let g:javascript_plugin_jsdoc = 1
    let g:javascript_plugin_ngdoc = 1


    " if hidden is not set, TextEdit might fail.
    set hidden

    " You will have bad experience for diagnostic messages when it's default 4000.
    set updatetime=300

    " don't give |ins-completion-menu| messages.
    set shortmess+=c

    " always show signcolumns
    set signcolumn=yes



    " Use tab for trigger completion with characters ahead and navigate.
    " Use command ':verbose imap <tab>' to make sure tab is not mapped by other plugin.
    inoremap <silent><expr> <TAB>
          \ pumvisible() ? "\<C-n>" :
          \ <SID>check_back_space() ? "\<TAB>" :
          \ coc#refresh()
    inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

    function! s:check_back_space() abort
      let col = col('.') - 1
      return !col || getline('.')[col - 1]  =~# '\s'
    endfunction



    " Use <c-space> to trigger completion.
    inoremap <silent><expr> <c-space> coc#refresh()

    " Use <cr> to confirm completion, `<C-g>u` means break undo chain at current position.
    " Coc only does snippet and additional edit on confirm.
    inoremap <expr> <cr> pumvisible() ? "\<C-y>" : "\<C-g>u\<CR>"

    " coc-yank
    nnoremap <silent> <space>y  :<C-u>CocList -A --normal yank<cr>

    " Use `[g` and `]g` to navigate diagnostics
    nmap <silent> [g <Plug>(coc-diagnostic-prev)
    nmap <silent> ]g <Plug>(coc-diagnostic-next)

    " Remap keys for gotos
    nmap <silent> gd <Plug>(coc-definition)
    nmap <silent> gy <Plug>(coc-type-definition)
    nmap <silent> gi <Plug>(coc-implementation)
    nmap <silent> gr <Plug>(coc-references)

    " Use K to show documentation in preview window
    nnoremap <silent> K :call <SID>show_documentation()<CR>

    function! s:show_documentation()
      if (index(['vim','help'], &filetype) >= 0)
        execute 'h '.expand('<cword>')
      else
        call CocAction('doHover')
      endif
    endfunction

    " Highlight symbol under cursor on CursorHold
    autocmd CursorHold * silent call CocActionAsync('highlight')

    " Remap for rename current word
    nmap <leader>rn <Plug>(coc-rename)

    " Remap for format selected region
    xmap <leader>f  <Plug>(coc-format-selected)
    nmap <leader>f  <Plug>(coc-format-selected)

    augroup mygroup
      autocmd!
      " Setup formatexpr specified filetype(s).
      autocmd FileType typescript,json setl formatexpr=CocAction('formatSelected')
      " Update signature help on jump placeholder
      autocmd User CocJumpPlaceholder call CocActionAsync('showSignatureHelp')
    augroup end

    " Remap for do codeAction of selected region, ex: `<leader>aap` for current paragraph
    xmap <leader>a  <Plug>(coc-codeaction-selected)
    nmap <leader>a  <Plug>(coc-codeaction-selected)

    " Remap for do codeAction of current line
    nmap <leader>ac  <Plug>(coc-codeaction)
    " Fix autofix problem of current line
    nmap <leader>qf  <Plug>(coc-fix-current)

    " Create mappings for function text object, requires document symbols feature of languageserver.

    xmap if <Plug>(coc-funcobj-i)
    xmap af <Plug>(coc-funcobj-a)
    omap if <Plug>(coc-funcobj-i)
    omap af <Plug>(coc-funcobj-a)

    " Use <tab> for select selections ranges, needs server support, like: coc-tsserver, coc-python
    nmap <silent> <TAB> <Plug>(coc-range-select)
    xmap <silent> <TAB> <Plug>(coc-range-select)
    xmap <silent> <S-TAB> <Plug>(coc-range-select-backword)

    " Use `:Format` to format current buffer
    command! -nargs=0 Format :call CocAction('format')

    " Use `:Fold` to fold current buffer
    command! -nargs=? Fold :call     CocAction('fold', <f-args>)

    " use `:OR` for organize import of current buffer
    command! -nargs=0 OR   :call     CocAction('runCommand', 'editor.action.organizeImport')

    " Add status line support, for integration with other plugin, checkout `:h coc-status`

    " Using CocList
    " Show all diagnostics
    nnoremap <silent> <space>a  :<C-u>CocList diagnostics<cr>
    " Manage extensions
    nnoremap <silent> <space>e  :<C-u>CocList extensions<cr>
    " Show commands
    nnoremap <silent> <space>c  :<C-u>CocList commands<cr>
    " Find symbol of current document
    nnoremap <silent> <space>o  :<C-u>CocList outline<cr>
    " Search workspace symbols
    nnoremap <silent> <space>s  :<C-u>CocList -I symbols<cr>
    " Do default action for next item.
    nnoremap <silent> <space>j  :<C-u>CocNext<CR>
    " Do default action for previous item.
    nnoremap <silent> <space>k  :<C-u>CocPrev<CR>
    " Resume latest coc list
    nnoremap <silent> <space>p  :<C-u>CocListResume<CR>




    "let ayucolor="mirage"
    "set bg=light
    set bg=dark

    "let g:gruvbox_italic = 1
    "let g:gruvbox_italicize_strings = 1
    "let g:gruvbox_filetype_hi_groups = 1
    "let g:gruvbox_plugin_hi_groups = 1
    colorscheme gruvbox9_soft
    "let g:onedark_terminal_italics=1
    "if (has("autocmd"))
      "augroup colorextend
        "autocmd!
        "" Make `Function`s bold in GUI mode
        "autocmd ColorScheme * call onedark#extend_highlight("Function", { "gui": "bold" })
        "" Override the `Statement` foreground color in 256-color mode
        "autocmd ColorScheme * call onedark#extend_highlight("Statement", { "fg": { "cterm": 128 } })
        "" Override the `Identifier` background color in GUI mode
        "autocmd ColorScheme * call onedark#extend_highlight("Identifier", { "bg": { "gui": "#333333" } })
      "augroup END
    "endif
    "colorscheme onedark


    fun! QuitSave()
      :mksession!
      :wviminfo loki.viminfo
    endfun
    augroup  quit
      au!
      au QuitPre * :call QuitSave()
    augroup END
    augroup  initProject
      au!
      au SessionLoadPost Session.vim :rviminfo loki.viminfo
    augroup END
    "Plugins for fun
    "Plug 'terryma/vim-multiple-cursors'
    "Plug 'mileszs/ack.vim'
    "Plug 'mhinz/vim-startify'
    "Plug 'jiangmiao/auto-pairs'
    "Plug 'dense-analysis/ale'
    "Plug 'zxqfl/tabnine-vim'
    "Plug 'Shougo/defx.nvim'
    "plug 'zefei/vim-wintabs'
    "plug 'zefei/vim-wintabs-powerline'
    "vim的配置真的是个无底洞，现在又出了新的补全，语法检查，要不是你打开文件快，我才懒得补你

1.
碰到一些兼容性问题，把插件配置都放到下面了，结果就是很难看。所以，还要稍微写下注释。
2.
wintab很好的实现了我对buffer，window和tab的理解，但是它有点重，所以我可能会自己写个小插件在现有插件的基础上实现这个功能。
3.
vim折腾起来是个无底洞，见好就收。
