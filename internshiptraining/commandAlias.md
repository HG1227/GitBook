# 命令别名存储

## 方法一 写bash函数

### 第一步 打开bash_profile或者zshrc文件

```angular2html
vim ~/.zshrc
```

### 第二步 将命令写到bash_profile或者zshrc中
```angular2html
gitacpp(){
    git add . && git commit -m "$1" && git pull && git push
}

hexocgd(){
    hexo clean && hexo g && hexo d
}
```

文件修改后如下

```angular2html
#sellrobbyrussel If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH=/Users/haomo/.oh-my-zsh

# Set name of the theme to load. Optionally, if you set this to "random"
# it'll load a random theme each time that oh-my-zsh is loaded.
# See https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
ZSH_THEME="robbyrussell"

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion. Case
# sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment the following line to disable bi-weekly auto-update checks.
# DISABLE_AUTO_UPDATE="true"

# Uncomment the following line to change how often to auto-update (in days).
# export UPDATE_ZSH_DAYS=13

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
# ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# The optional three formats: "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load? (plugins can be found in ~/.oh-my-zsh/plugins/*)
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git)

source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# ssh
# export SSH_KEY_PATH="~/.ssh/rsa_id"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"

export PATH=$PATH:/Applications/android-sdk-macosx/tools:/Applications/android-sdk-macosx/platform-tools

#THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
export SDKMAN_DIR="/Users/haomo/.sdkman"
[[ -s "/Users/haomo/.sdkman/bin/sdkman-init.sh" ]] && source "/Users/haomo/.sdkman/bin/sdkman-init.sh"

export PATH="$HOME/.yarn/bin:$PATH"

gitacpp(){
	git add . && git commit -m "$1" && git pull && git push
}

hexocgd(){
	hexo clean && hexo g && hexo d
}
```

## 方法二 写alias

alias可以简化一些复杂的命令串，使一个单词或简化后的命令即可实现复杂（通常是带很多参数的长串）命令。

### 基本用法

```angular2html
alias 简化命令=‘实际的长串命令’    //实际长串命令通常为‘原命令 -/选项参数’
```

```angular2html
alias gitacpp = 'git add . && git commit -m "$1" && git pull && git push' 
alias hexocgd = 'hexo clean && hexo g && hexo d' 
```
- 注意:此方法只能在当前窗口使用 关机重启后便被清除

### 获取别名

```angular2html
alias        //即可查看当前设定的所有alias别名
```

### 取消别名

```angular2html
unalias 简化命令
```

------

### 永久生效

直接使用alias命令定义的别名，重启后就会失效。因此如果需要永久使用别名，就需要做一些操作。

修改/定义别名，实际上也是在定义系统的环境变量。

系统环境变量文件是/etc/profile。

但是查看profile文件，你会发现文件最开头就有提示：

![alias存储提示](assets/commandAlias1.png)

因此最好不要直接在/etc/profile文件出进行定义，而是在/etc/bashrc中进行定义，定义完成后，通过    #source /etc/bashrc使其生效。

或者，重新定义一个文件 /etc/profile.d/alias_bash.sh （alias_bash文件名是任意取的），然后通过    #source /etc/profile.d/alias_bash使其生效。

通过这个方法，就可以使自己（自定义）的别名永久生效了。