# Zettelkasten

This is my personal zettelkasten based on the work of [Niklas Luhmann](https://en.wikipedia.org/wiki/Niklas_Luhmann). It all started after reading Edmun Wenick's post [building a note-taking system with vanilla vim](https://www.edwinwenink.xyz/posts/42-vim_notetaking/). All the way towards the end, he mentions that the folder structure soon became too compicated and instead he plans to allow for organic growth zettelkasten style. ~~Hours~~ Days later after going down the multiple ~~layers of hell~~ rabbit holes, I settled using [Vimwiki](https://github.com/vimwiki) with the [vim-zettel](https://github.com/michal-h21/vim-zettel) plugin.

## Inspiration

The following sources have been influential in the creatation and structure of my zettelkasten.
- [Zettelkasten.de](https://zettelkasten.de)
- [How to Take Smart Notes](https://takesmartnotes.com)
- [r/Zettelkasten](https://www.reddit.com/r/Zettelkasten/)
- [The Zettelkasten Manifesto](https://www.youtube.com/watch?v=c5Tst3-zcWI)

## Configuration

I added the `.md` wehn vimwiki creates a new file. This allows links to be clickable when using [zettle](https://www.zettlr.com). In addition to vimwiki :tags: I also add #tags. While it doubles the work each time I add tags, it allows me to seach tags directly in vim and use the tag feature in zettlr.

In addition to vimwiki and vim-zettel I have added a few couple more plugins to make the writing expereince more enjoyable: [Pencil](https://github.com/reedes/vim-pencil), [Goyo](https://github.com/junegunn/goyo.vim). 

The relevant portions of my .vimrc are found below.

```
"vimwiki and vim-zettel stuff
set nocompatible
filetype plugin on
syntax on
let g:zettel_format = "%Y%m%d%H%M"
let g:vimwiki_list = [{'path': '~/path/to/zettelkasten/', 'syntax': 'markdown', 'ext': '.md'}]
let g:vimwiki_markdown_link_ext = 1
let g:vimwiki_ext2syntax = {'.md': 'markdown', '.markdown': 'markdown', '.mdown': 'markdown'}
let g:nv_search_paths = ['~/path/to/Zettelkasten']
let g:zettel_options = [{"front_matter" : [["tags", ""], ["citation", ""]]}]
let g:zettel_fzf_command = "rg --column --line-number --ignore-case --no-heading --color=always "
let g:vimwiki_folding = 'expr'
nnoremap <leader>zn :ZettelNew<space>

" Pencil stuff
let g:pencil#wrapModeDefault = 'soft'   " default is 'hard'
augroup pencil
  autocmd!
  autocmd FileType markdown,mkd call pencil#init()
  autocmd FileType text         call pencil#init({'wrap': 'hard'})
augroup END

" Goyo stuff
function! s:goyo_enter()
  set nonumber
  set nornu
endfunction

function! s:goyo_leave()
  set number
  set rnu
endfunction

autocmd! User GoyoEnter nested call <SID>goyo_enter()
autocmd! User GoyoLeave nested call <SID>goyo_leave()

" plugins
call plug#begin()
    Plug 'vimwiki/vimwiki'
    Plug 'junegunn/fzf'
    Plug 'junegunn/fzf.vim'
    Plug 'junegunn/goyo.vim'
    Plug 'michal-h21/vim-zettel'
    Plug 'tpope/vim-fugitive'
    Plug 'reedes/vim-pencil'
call plug#end()
```
