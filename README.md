# nvim-lilypond-suite

This is a plugin ([Neovim](https://github.com/neovim/neovim) only) for writing [LilyPond](https://lilypond.org/index.html) scores, with asynchronous make, midi/MP3 player, "hyphenation" function for lyrics, fast syntax highlighting... This repository also contains an ftplugin for **LaTeX** files which allows embedded LilyPond syntax highlighting, and makeprg which support `lilypond-book` or `lyluatex` package out of the box.

<p align=center>
   <a href="https://github.com/martineausimon/nvim-lilypond-suite/wiki/1.-Installation">Installation</a> • <a href="https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration">Configuration</a> • <a href="https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage">Usage</a> • <a href="https://github.com/martineausimon/nvim-lilypond-suite/wiki/4.-Tips-and-tricks">Tips & tricks</a>
</p>

## FEATURES

* **Fast syntax file for LilyPond**
* **Asynchronous :make** - compile in background without freezing Neovim
* **mp3 player in floating window** (LilyPond only) - convert and play midi file while writing score (using `mpv`, `fluidsynth` & `ffmpeg`)
* **QuickPlayer** (LilyPond only) - convert and play only visual selection
* **Hyphenation** : automatically place hyphens ' **--** ' inside texts to make those texts usable as lyrics (LilyPond only)
* **Simple ftplugin for LilyPond** with `makeprg`, correct `errorformat`
* **Compile only main file when working on multiple files project** (LilyPond only)
* **ftplugin for TeX files** whith detect and allows embedded LilyPond syntax, adaptive `makeprg` function for `lyluatex` or `lilypond-book`, correct `errorformat`
* **Easy auto-completion and Point & Click configuration**

<p align="center">
<img src="https://user-images.githubusercontent.com/89019438/191845626-4ba6224c-46c3-484f-a355-5cf10a66889f.png">
</p>

## QUICK INSTALL WITH CONFIG

> **⚠ This plugin requires Nvim >= 0.7**

If you want to use all the functions (player, hyphenation for various languages...), please read the [installation section](https://github.com/martineausimon/nvim-lilypond-suite/wiki/1.-Installation) in the wiki to install dependencies

### [packer.nvim](https://github.com/wbthomason/packer.nvim)

```lua 
use { 'martineausimon/nvim-lilypond-suite',
  requires = { 'MunifTanjim/nui.nvim' },
  config = function()
    require('nvls').setup({
      lilypond = {
        mappings = {
          player = "<F3>",
          compile = "<F5>",
          open_pdf = "<F6>",
          switch_buffers = "<A-Space>",
          insert_version = "<F4>",
          hyphenation = "<F12>",
          hyphenation_change_lang = "<F11>",
          insert_hyphen = "<leader>ih",
          add_hyphen = "<leader>ah",
          del_next_hyphen = "<leader>dh",
          del_prev_hyphen = "<leader>dH",
          del_selected_hyphen = "<leader>dh"
        },
        options = {
          pitches_language = "default",
          output = "pdf",
          main_file = "main.ly",
          main_folder = "%:p:h",
          hyphenation_language = "en_DEFAULT",
        },
      },
      latex = {
        mappings = {
          compile = "<F5>",
          open_pdf = "<F6>",
          lilypond_syntax = "<F3>"
        },
        options = {
          clean_logs = false
        },
      },
      player = {
        mappings = {
          quit = "q",
          play_pause = "p",
          loop = "<A-l>",
          backward = "h",
          small_backward = "<S-h>",
          forward = "l",
          small_forward = "<S-l>",
          decrease_speed = "j",
          increase_speed = "k",
          halve_speed = "<S-j>",
          double_speed = "<S-k>"
        },
        options = {
          row = "2%",
          col = "99%",
          width = "37",
          height = "1",
          border_style = "single",
          winhighlight = "Normal:Normal,FloatBorder:Normal",
          mpv_flags = {
            "--msg-level=cplayer=no,ffmpeg=no",
            "--loop",
            "--config-dir=/dev/null"
          }
        },
      },
    })
  end
}
```

## WIKI INDEX

* [Home](https://github.com/martineausimon/nvim-lilypond-suite/wiki)
* [Installation](https://github.com/martineausimon/nvim-lilypond-suite/wiki/1.-Installation)
  * [nvim-lilypond-suite plugin](https://github.com/martineausimon/nvim-lilypond-suite/wiki/1.-Installation#nvim-lilypond-suite-plugin)
  * [Dependences](https://github.com/martineausimon/nvim-lilypond-suite/wiki/1.-Installation#dependences)
    * [midi/mp3 player](https://github.com/martineausimon/nvim-lilypond-suite/wiki/1.-Installation#midimp3-player)
    * [Hyphenation function](https://github.com/martineausimon/nvim-lilypond-suite/wiki/1.-Installation#hyphenation-function)
* [Configuration](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration)
  * [Customize default settings](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#customize-default-settings)
  * [Per-folder configuration](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#per-folder-configuration)
  * [Highlightings](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#highlightings)
    * [Recommended syntax sync settings](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#recommended-syntax-sync-settings)
    * [Highlight groups](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#highlight-groups)
    * [Highlight pitches for others languages](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#highlight-pitches-for-others-languages)
    * [Lighter syntax highlighting](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#lighter-syntax-highlighting)
  * [Error messages](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#error-messages)
  * [Auto-completion](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#auto-completion)
    * [Recommended settings](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#recommended-settings)
    * [Dictionary files](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#dictionary-files)
    * [My current config](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#my-current-config)
  * [Point and click](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#point-and-click)
    * [Neovim remote](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#neovim-remote)
    * [Configure point and click](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#configure-the-point-and-click)
    * [Pdf reader](https://github.com/martineausimon/nvim-lilypond-suite/wiki/2.-Configuration#pdf-reader)
* [Usage](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage)
  * [Mappings & commands](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#mappings--commands)
    * [LilyPond](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#lilypond)
    * [LaTex](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#latex)
    * [Player (LilyPond only)](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#player-mappings-lilypond-only)
  * [Hyphenation function](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#hyphenation-function)
    * [Default language](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#default-language)
    * [Others languages](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#other-languages)
    * [Output comparaison](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#outputs-comparaison)
  * [Multiple files projects](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#multiple-files-projects)
  * [LaTex](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#latex-1)
    * [lilypond-book or lyluatex](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#lilypond-book-or-lyluatex)
    * [Clean log files on exit](https://github.com/martineausimon/nvim-lilypond-suite/wiki/3.-Usage#clean-log-files-on-exit)
* [Tips and tricks](https://github.com/martineausimon/nvim-lilypond-suite/wiki/4.-Tips-and-tricks)
  * [LaTex](https://github.com/martineausimon/nvim-lilypond-suite/wiki/4.-Tips-and-tricks#latex)
    * [Justify score with lilypond-book](https://github.com/martineausimon/nvim-lilypond-suite/wiki/4.-Tips-and-tricks#justify-score-with-lilypond-book)
    * [Adjust spaces between systems](https://github.com/martineausimon/nvim-lilypond-suite/wiki/4.-Tips-and-tricks#adjust-spaces-between-systems)
  * [Others](https://github.com/martineausimon/nvim-lilypond-suite/wiki/4.-Tips-and-tricks#others)
    * [Compile automatically on save](https://github.com/martineausimon/nvim-lilypond-suite/wiki/4.-Tips-and-tricks#compile-automatically-on-save)
