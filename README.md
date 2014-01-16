# Vim motion on speed! [![Build Status](https://travis-ci.org/haya14busa/vim-easymotion.png?branch=master)](https://travis-ci.org/haya14busa/vim-easymotion)

![two-character key](http://homes.cs.washington.edu/~supasorn/easymotion.gif)

Original: [Lokaltog/vim-easymotion](https://github.com/Lokaltog/vim-easymotion)

I forked Lokaltog's vim-easymotion and currently maintain it. Fix some bugs,
add new features (based on supasorn's work and others), and improve some function.

I greatly appreciate Lokaltog's and others' works!

# Introduction

EasyMotion provides a much simpler way to use some motions in vim. It
takes the `<number>` out of `<number>w` or `<number>f{char}` by
highlighting all possible choices and allowing you to press one key to
jump directly to the target.

When one of the available motions is triggered, all visible text
preceding or following the cursor is faded, and motion targets are
highlighted.

EasyMotion is triggered by one of the provided mappings.

# Important notes about the default bindings

**The default leader has been changed to `<Leader><Leader>` to avoid
conflicts with other plugins you may have installed.** This can easily be
changed back to pre-1.3 behavior by rebinding the leader in your vimrc:

	map <Leader> <Plug>(easymotion-prefix)

All motions are now triggered with `<Leader><Leader>` by default, e.g.
`<Leader><Leader>t`, `<Leader><Leader>gE`.

# Usage example

Type `<Leader><Leader>w` to trigger the word motion `w`. When the motion is
triggered, the text is updated (no braces are actually added, the text
is highlighted in red by default):

	<cursor>Lorem {a}psum {b}olor {c}it {d}met.

Press `c` to jump to the beginning of the word "sit":

	Lorem ipsum dolor <cursor>sit amet.

Similarly, if you're looking for an "o", you can use the `f` motion.
Type `<Leader><Leader>fo`, and all "o" characters are highlighted:

	<cursor>L{a}rem ipsum d{b}l{c}r sit amet.

Press `b` to jump to the second "o":

	Lorem ipsum d<cursor>olor sit amet.

Jeffrey Way of Nettuts+ has also [written
a tutorial](http://net.tutsplus.com/tutorials/other/vim-essential-plugin-easymotion/)
about (Lokaltog's) EasyMotion.

# Animated demonstration

![Animated demonstration](http://oi54.tinypic.com/2yysefm.jpg)

# New feature
Modifications to Lokaltog's EasyMotion

## Two key combo
1. Use one - two character key jump. Display two keys if one-character key is not enough, so you can see what two keys to type without waiting after pressing the first key.

![two-character key](http://homes.cs.washington.edu/~supasorn/easymotion.gif)

## Bidirectional search
Added forward-backward search (bidirectional) search. You can jump forward or backward at the same time by `<Leader>s`. One useful trick is to map `map <SPACE> <Plug>(easymotion-s)` to use space bar instead and save one keystroke!

## Find target by smartcase!

Matching target keys by smartcase. You can type targets more lazily.

Type `<Leader><Leader>sv`, and all "v" and "V" characters are highlighted:

	<cursor>V{a}im v{b}im V{c}IM.

Press `b` to jump to the second "v":

	Vim <cursor>vim VIM.

Type `<Leader><Leader>sV`, and all "V" characters are highlighted, not "v":

	<cursor>V{a}im vim V{b}IM.

Press `b` to jump to the second "V":

	Vim vim <cursor>VIM.

Add following description in your vimrc:

	let g:EasyMotion_smartcase = 1

Default:0

## Migemo feature (for Japanese user)
Easymotion can match multibyte Japanese character with a alphabet input.
For example, '<Leader><Leader>fa' can search 'あ'.
This feature doesn't require cmigemo because Easymotion includes regex
patterns generated by cmigemo.

Add following description in your vimrc:

	let g:EasyMotion_use_migemo = 1

Default:0

## Keep cursor column
Added keep cursor column option when JK motion.

Add following description in your vimrc:

	let g:EasyMotion_startofline = 0

Default:0

## Jump to anywhere!
JumpToAnywhere motion!

Add following description in your vimrc and you can customize this behavior:

	map <Space><Space> <Plug>(easymotion-jumptoanywhere)
	let g:EasyMotion_re_anywhere = '\v' .
		\  '(<.|^)' . '|' .
		\  '(.$)' . '|' .
		\  '(\l)\zs(\u)' . '|' .
		\  '(_\zs.)' . '|' .
		\  '(/\zs.)' . '|' .
		\  '(#\zs.)'

## Select line
Added SelectLines function which allows you to select any range of lines using two consecutive easymotion calls. Default mappings are `c<Leader>l, d<Leader>l, v<Leader>l, y<Leader>l`(set `let g:EasyMotion_do_special_mapping = 1`, this function is disabled by default).

To yank a single line you can either type the same character(s) twice, or use '.' character. E.g. `vlb.` will select the line with character 'b'.

Note: to promote good Vim habits, you should learn standard movement commands like `}}, vi(, va(, %, ][, ]], [(, etc.` before resorting to this function.

Select lines using `v<Leader>l`

![two-character key](http://homes.cs.washington.edu/~supasorn/easymotion2.gif)

Yank lines using `y<Leader>l`. You can copy lines without moving cursor back and forth between line you want to yank and line you want to paste.

![two-character key](http://homes.cs.washington.edu/~supasorn/easymotion3.gif)

## Select Phrase
(Experimental) Added SelectPhrase function which allows you to make selection between any two characters. Default mapping are `c<Leader>p, d<Leader>p, v<Leader>p, y<Leader>p`.(set `let g:EasyMotion_do_special_mapping = 1`, this function is disabled by default)

Example usage: type `v<Leader>p` then press two input characters. Now the two input characters will be highlight on the same screen, and you can then type two combos to make selection.

## \<Plug\> mapping support
But I keep backward compatibility, so you can easily move to new easymotion.

With this `<Plug>` support, I can easily implement new mapping without
confliction.Such as

- `<Plug>(easymotion-bd-w)`
  - (bidirectional word motion)
- `<Plug>(easymotion-jumptoanywhere)`
- and others! See :h easymotion-more-mapping


Pull requests are welcome! :)
