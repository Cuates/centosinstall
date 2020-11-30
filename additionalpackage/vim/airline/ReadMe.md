# airline
> Vim And Airline

## Table of Contents
* [Important Note](#important-note)
* [Prerequisite Powerlevel10K](#prerequisite-powerlevel10k)
* [Install And Configure](#install-and-configure)

### **Important Note**
* The instructions were written with Vim 8+

### Prerequisite Powerlevel10K
* [powerlevel10k]()

### Install And Configure
[Vundle Vim](https://github.com/VundleVim/Vundle.vim)<br />
[Vim Airline](https://github.com/vim-airline/vim-airline)<br />
[Vim Airline Themes](https://github.com/vim-airline/vim-airline-themes)<br />
[Vim Airline Screenshots](https://github.com/vim-airline/vim-airline/wiki/Screenshots)<br />
[One Half Vim](https://github.com/sonph/onehalf/tree/master/vim)<br />
[Change Color Schemes In Vim](https://linoxide.com/tools/change-color-schemes-in-vim/)<br />
[Vim Colors](https://vimcolors.com/)<br />
[Vim Colors Archman](https://vimcolors.com/1183/archman/dark)<br />
[Vim Colors Hyper](https://vimcolors.com/1176/hyper/dark)<br />
[Vim Colors Srcery](https://vimcolors.com/469/srcery/dark)<br />
[Vim Colors Xcode Dark](https://vimcolors.com/1157/xcodedark/dark/)<br />
[Vim Colors Xcode Dark HC](https://vimcolors.com/1192/xcodedarkhc/dark)<br />
[Vim Colors Escuro](https://vimcolors.com/878/escuro/dark)<br />
[Vim Colors Horizon](https://vimcolors.com/920/horizon/dark)<br />
[Vim Colors Medic Chalk](https://vimcolors.com/1206/medic_chalk/dark)<br />
[Vim Colors Visual Studio Dark](https://vimcolors.com/734/VisualStudioDark/dark)<br />
[Converting Tabs To Spaces](https://vim.fandom.com/wiki/Converting_tabs_to_spaces)<br />
[Vim Convert Tabs To Spaces](https://howchoo.com/g/m2u0nthkyti/vim-convert-tabs-to-spaces)<br />
[How To Show Line Numbers In Vim](https://linuxize.com/post/how-to-show-line-numbers-in-vim/)<br />
[Preser Vim Nerd Tree](https://github.com/preservim/nerdtree)<br />
[Space Vim Nerd Tree](https://github.com/SpaceVim/nerdtree)<br />
[Adding Custom Vim Colorscheme In Mac OS Sierra](https://stackoverflow.com/questions/47980152/adding-custom-vim-colorscheme-in-macos-sierra)

* Set up Vundle
  * `git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`
* Configure Plugins
  * If .vimrc is not created, then create one for modifications with airline
    * `vim ~/.vimrc`
      * Paste the following into the .vimrc file
        * <pre>
          set nocompatible              " be iMproved, required
          filetype off                  " required

          " set the runtime path to include Vundle and initialize
          set rtp+=~/.vim/bundle/Vundle.vim
          call vundle#begin()
          " alternatively, pass a path where Vundle should install plugins
          "call vundle#begin('~/some/path/here')

          " let Vundle manage Vundle, required
          Plugin 'VundleVim/Vundle.vim'

          " The following are examples of different formats supported.
          " Keep Plugin commands between vundle#begin/end.
          " plugin on GitHub repo
          Plugin 'tpope/vim-fugitive'

          " plugin from http://vim-scripts.org/vim/scripts.html
          " Plugin 'L9'
          " Git plugin not hosted on GitHub
          Plugin 'git://git.wincent.com/command-t.git'

          " git repos on your local machine (i.e. when working on your own plugin)
          " Plugin 'file:///home/<username>/path/to/plugin'
          " The sparkup vim script is in a subdirectory of this repo called vim.
          " Pass the path to set the runtimepath properly.
          Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}

          " Install L9 and avoid a Naming conflict if you've already installed a
          " different version somewhere else.
          " Plugin 'ascenator/L9', {'name': 'newL9'}

          " Airline
          Plugin 'vim-airline/vim-airline'

          " Airline themes
          Plugin 'vim-airline/vim-airline-themes'

          " NERDTree
          Plugin 'preservim/nerdtree'

          " All of your Plugins must be added before the following line
          call vundle#end()            " required
          filetype plugin indent on    " required

          " To ignore plugin indent changes, instead use:
          "filetype plugin on
          "
          " Brief help
          " :PluginList       - lists configured plugins
          " :PluginInstall    - installs plugins; append `!` to update or just
          " :PluginUpdate
          " :PluginSearch foo - searches for foo; append `!` to refresh local cache
          " :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
          "
          " see :h vundle for more details or wiki for FAQ
          " Put your non-Plugin stuff after this line

          " Vim settings
          colorscheme xcodedarkhc
          syntax on
          set t_Co=256
          " set number " Optional
          set tabstop=2
          set shiftwidth=2
          set expandtab

          " Set new path
          set runtimepath+=~/.vim/colors

          " Set encoding to utf-8
          set encoding=utf-8

          " Check if symbol does not exist before proceeding
          if !exists('g:airline_symbols')
            let g:airline_symbols = {}
          endif

          " Get powerline fonts
          let g:airline_powerline_fonts = 1

          " Powerline symbols
          let g:airline_left_sep = '' " (right facing solid triangle)
          let g:airline_left_alt_sep = '' " (right facing angle bracket)
          let g:airline_right_sep = '' " (left facing solid triangle)
          let g:airline_right_alt_sep = '' " (right facing angle bracket)
          let g:airline_symbols.branch = '' " (git branch)
          let g:airline_symbols.readonly = '' " (lock)
          let g:airline_symbols.maxlinenr = '' " (line number)
          let g:airline_symbols.dirty='⚡ ' " (thunder bolt)

          " Unicode symbols
          let g:airline_left_sep = '»'
          let g:airline_left_sep = '' " (right facing solid triangle)
          let g:airline_right_sep = '«'
          let g:airline_right_sep = '' " (left facing solid triangle)
          let g:airline_symbols.linenr = '¶ '
          let g:airline_symbols.maxlinenr = ''
          let g:airline_symbols.paste = 'ρ'
          let g:airline_symbols.paste = 'Þ'
          let g:airline_symbols.whitespace = 'Ξ'

          " Tabline
          let g:airline#extensions#tabline#enabled = 1
          let g:airline#extensions#tabline#show_splits = 1
          let g:airline#extensions#tabline#show_tabs = 1
          let g:airline#extensions#tabline#show_tab_type = 1
          let g:airline_theme='jellybeans'

          " Close vim when NERDTree is the only window opened
          autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endifautocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
          </pre>
    * Save and Exit
* Install NERDTree
  * `git clone https://github.com/preservim/nerdtree.git ~/.vim/bundle/nerdtree`
    * Make sure the following NERDTree is in the .vimrc file
      * <pre>
        " NERDTree
        Plugin 'preservim/nerdtree'
        </pre>
    * Make sure the close NERDTree when it is the only window opened
      * <pre>
        " Close vim when NERDTree is the only window opened
        autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endifautocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
        </pre>
* Install Plugins:
  * Launch vim
    * run
      * `:PluginInstall`
  * Exit vim once done
* Download themes to theme folder
  * `git clone https://github.com/vim-airline/vim-airline-themes`
    * Move all themes to the folder
      * `mv vim-airline-themes/autoload/airline/themes/* ~/.vim/bundle/vim-airline/autoload/airline/themes/`
    * To use any of the themes downloaded open up vim and type the command in the statusline
      * Test theme proceed with the following command
        * Open vim
          * `:AirlineTheme <theme>`
      * To make the theme permanent add the following line to .vimrc if not already done so
        * `let g:airline_theme='jellybeans'`
* Vim View and change default color scheme
  * All your customizing is supposed to happen in $HOME/.vimrc and/or $HOME/.vim/ and nowhere else
    * Create a vim color folder
      * `mkdir ~/.vim/colors/`
    * Make sure .vimrc has the runtimepath set to your new color location
      * <pre>
        " Set new path
        set runtimepath+=~/.vim/colors
        </pre>
  * Navigate to the following directory for out of the box themes
    * `cd /usr/share/vim/vim*/colors directory`
  * Copy entire vim themes from system director to local directory
    * NOTE vim number may vary
    * `cp /usr/share/vim/vim80/colors/*.vim ~/.vim/colors`
  * To see a list of ready-to-use themes, open any document using the Vim editor, use
    * `:colorscheme [space] [crtl+d]`
  * For instance, to switch to the color scheme darkblue, open any document using the Vim editor, use
    * `:colorscheme darkblue`
  * Download another theme and use it
    * **NOTE vim number will depend on the version of vim you have installed (In this case it is 81)**
    * git clone https://github.com/arzg/vim-colors-xcode.git
      * Move the scheme configuration to ~/.vim/colors/
        * `mv vim-colors-xcode/colors/*.vim  ~/.vim/colors/`
      * * Open any document using the Vim editor and search for xcodedarkhc, use
        * `:colorscheme <colorscheme_name>`
      * To make this change permanent, update .vimrc file in /etc or in the user's home directory.
        * Change below the line with your preferred color scheme name:
          * `colorscheme <colorscheme_name>`
        * To enable the syntax highlight, use:
          * `syntax on`
