# BÉPO et vim

Pour cet article dedié à bépo, je vais utiliser la langue de Molière puisqu'il y a peu de chances qu'un anglophone utilise un clavier ergonomique conçu pour le français.

Quand j'ai commencé à utiliser bépo, j'utilisais Spacemacs comme éditeur de texte. À ma grande surprise cela s'est fait sans problème. Installation du package, configuration par défaut, terminé. Tous les packages que j'utilisais étaient bien supportés.

Mais il y a quelque semaines, j'ai décidé de redonner sa chance à mon premier coup de cœur: Neovim. Je dois avouer que cela ne s'est pas fait sans lorgner quelques semaines sur les tweets alléchants de [phaazon](https://twitter.com/phaazon_/status/1249478873424842753). Sachant qu'il utilise déjà bépo, j'ai récupéré sa [config](https://github.com/phaazon/config/tree/master/nvim) et go.

Après quelques semaines, ce qui devait arriver arriva. Nouveaux plugins, aucune compatibilité avec bépo. Rebonjour les soirées à lire des docs. Rebonjour les plugins dont aucune conf ne se ressemble.

Du coup, j’ai décidé de rassembler ici mes notes pour configurer tel ou tel plugin qu'il me semble important d'avoir sur un éditeur de texte moderne.

## Les conf de base

Le [site officiel](https://bepo.fr/wiki/Vim#.7E.2F.vimrc) de bépo fournit un remapage de base pour vim qui fonctionne très bien. C'est par là qu'il faut commencer.

## Fugitive

[Fugitive](https://github.com/tpope/vim-fugitive) est le meilleur client Git pour vim. Malheureusement, par défaut, la touche `s` place le fichier sous le curseur en staging. Je passe les multiples pétages de câbles sous silence.

```
" fugitive
Plug 'tpope/vim-fugitive'
let g:nremap = { 's': 'S' } " use S to stage current file
```

## Vim-visual-multi

[vim-visual-multi](https://github.com/mg979/vim-visual-multi) est la plus récente tentative stable d'implémenter les multis curseurs sur vim. Franchement, ça marche bien. Mais c’est fait au détriment de pas mal de hacks. La conséquence est que dans le mode multicurseurs, tous les remaps bépo (partie 1) ne fonctionnent pas. Du coup, conf:

```
" vim-visual-multi
Plug 'mg979/vim-visual-multi', {'branch': 'master'}
let g:VM_custom_motions = {
      \ 'c': 'h',
      \ 't': 'k',
      \ 's': 'j',
      \ 'r': 'l',
      \ 'é': 'w',
      \ 'É': 'W',
      \ 'J': 'T'
      \ }
let g:VM_custom_noremaps = {
      \ 't': 'j',
      \ 'T': 'J',
      \ 's': 'k'
      \ }
let g:VM_maps = {
      \ "Select Cursor Down": '<C-T>',
      \ "Select Cursor Up" : '<C-S>',
      \ }

```

C’est pas parfait mais l'essentiel y est.

## Fzf

Est-ce qu'on a encore besoin de présenter [fzf])(https://github.com/junegunn/fzf.vim) ? Le best fuzzy finder du quartier. Ici, je veux naviguer avec `ctrl-t` et `ctrl-s`.

```
autocmd FileType fzf tnoremap <buffer> <C-t> <Down>
autocmd FileType fzf tnoremap <buffer> <C-s> <Up>
```

## vim-easymotion

[vim-easymotion](https://github.com/easymotion/vim-easymotion) est un super outil pour se déplacer dans un fichier à toute vitesse. Les raccourcis par défaut son basés sur qwerty donc il faut évidemment faire un setup:

```

" easymotion
Plug 'easymotion/vim-easymotion'
let g:EasyMotion_keys = 'etisuranovpdlbjqxgyhf'
let g:EasyMotion_do_mapping = 0

```

```

```
