# Neovim setup for python developers (Linux, python 3.6+) :sunglasses:


## Install Neovim
You can install neovim following the instructions in their official page -
https://github.com/neovim/neovim/wiki/Installing-Neovim


## Install vim-plug plugin manager
```
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```
You can find the vim-plug usage details and commands here - 
https://github.com/junegunn/vim-plug


## Config file
Create a config file to store all the configurations(Appearance, plugins, keybindings, etc) for neovim.
```
touch ~/.config/nvim/init.vim
```

## Prepare python environment
In order for auto-complete, syntax check and formatter features to work for python, you need to install the below packages -
```
pip install pynvim
pip install jedi
pip install flake8
pip install autopep8
```
In case if you are using venv or anaconda, install all these packages in all your envs.


## Install neovim plugins
1. Edit the `~/.config/nvim/init.vim` file and paste the following lines of code -
```
set encoding=utf-8
set number
syntax enable
set noswapfile
set relativenumber
set scrolloff=7
set backspace=indent,eol,start

set tabstop=4
set softtabstop=4
set shiftwidth=4
set expandtab
set autoindent
set fileformat=unix

let mapleader = ' '

call plug#begin('~/.vim/plugged')
Plug 'morhetz/gruvbox'
Plug 'jiangmiao/auto-pairs'
Plug 'scrooloose/nerdtree'
Plug 'preservim/nerdcommenter'
Plug 'norcalli/nvim-colorizer.lua'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'tpope/vim-commentary'
" syntax check
Plug 'w0rp/ale'
" Autocomplete
Plug 'ncm2/ncm2'
Plug 'roxma/nvim-yarp'
Plug 'ncm2/ncm2-bufword'
Plug 'ncm2/ncm2-path'
Plug 'ncm2/ncm2-jedi'
" Formater
Plug 'Chiel92/vim-autoformat'
call plug#end()

" NCM2
augroup NCM2
  autocmd!
  " enable ncm2 for all buffers
  autocmd BufEnter * call ncm2#enable_for_buffer()
  " :help Ncm2PopupOpen for more information
  set completeopt=noinsert,menuone,noselect
  " When the <Enter> key is pressed while the popup menu is visible, it only
  " hides the menu. Use this mapping to close the menu and also start a new line.
  inoremap <expr> <CR> (pumvisible() ? "\<c-y>\<cr>" : "\<CR>")
  " uncomment this block if you use vimtex for LaTex
  " autocmd Filetype tex call ncm2#register_source({
  "           \ 'name': 'vimtex',
  "           \ 'priority': 8,
  "           \ 'scope': ['tex'],
  "           \ 'mark': 'tex',
  "           \ 'word_pattern': '\w+',
  "           \ 'complete_pattern': g:vimtex#re#ncm2,
  "           \ 'on_complete': ['ncm2#on_complete#omni', 'vimtex#complete#omnifunc'],
  "           \ })
augroup END

" Ale
let g:ale_lint_on_enter = 0
let g:ale_lint_on_text_changed = 'never'
let g:ale_echo_msg_error_str = 'E'
let g:ale_echo_msg_warning_str = 'W'
let g:ale_echo_msg_format = '[%linter%] %s [%severity%]'
let g:ale_linters = {'python': ['flake8']}

" Appearance
colorscheme gruvbox
let g:airline_theme='gruvbox'

if (has("termguicolors"))
    set termguicolors
endif

lua require 'colorizer'.setup()

" NerdTree
let NERDTreeQuitOnOpen=1
let g:NERDTreeMinimalUI=1
nmap <F2> :NERDTreeToggle<CR>

" Tabs
let g:airline#extensions#tabline#enabled=1
let g:airline#extensions#tabline#fnamemode=':t'
nmap <leader>1 :bp<CR>
nmap <leader>2 :bn<CR>
nmap <C-w> :bd<CR>
```


2. Open `nvim` and install plugins with the commands -
```
:PlugInstall
```
Close and reopen `nvim` and all the plugins should be working.

## Important key bindings
```
F2        -->       Open/close project tree view
Space+1   -->       Go to the previous file tab
Space+2   -->       Go to the next file tab
:bd       -->       Close current file tab
gcc       -->       Comment/uncomment current line
gc        -->       Comment/uncomment the entire block (Visual block mode)
```

## Screenshot
![Neovim look after setup](/hello_world_py.png)


Happy coding!!:fire: :rocket:
