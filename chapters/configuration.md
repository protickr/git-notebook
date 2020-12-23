# Git configuration

\
_**Retrieve installed git version**_  
>`$ git --version`  

_**Set git author's username and email**_  
>`$ git config --global user.name "user_name"`  
>`$ git config --global user.email "email"`  

_**all configuration list**_  
>`$ git config --list`  
>`$ git config --local --list`  
>`$ git config --global --list`  


_**help/doc of any command**_  
>`$ git help <command_verb>`  
or  
>`$ git <command_verb> --help`  
>`$ git <command_verb> -h`  
(shows short help doc)  
> 

_**Ignore files**_  
Add files, directories and wild-card entries to .gitignore file, files/directories listed in it will be ignored by git.  

_**Configure how git should handle end of line(EOL)**_  
Different for windows and Unix, e.g.,
> `$ git config --global core.autocrlf true` (for windows)  
> `$ git config --global core.autocrlf input` (for UNIX)  

_**Set default config editor for git**_  
First set intended app's path in your environment variables.  
> `$ git config --global core.editor "app --wait"`  
(Open config file in "app" and edit global-config by,)  
> `$ git config --global -e`

_**git diff and mergetool**_  
Set diff and merge tool as it is helpful while viewing differences and resolving merge conflicts graphically.  In this example we will be using "meld"   

_difftool_
> `$ git config --global diff.tool meld`  
> `$ git config --global difftool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"`  
(or set application path in environment variable and skip previous line)  
> `$ git config --global difftool.meld.cmd 'meld "$LOCAL" "$REMOTE"'`  
> `$ git config --global difftool.prompt true`  
> `$ git difftool`  
(shows differences graphically in meld app)

_mergetool_
> `$ git config --global merge.tool meld`  
> `$ git config --global mergetool.meld.path "C:\Program Files (x86)\Meld\Meld.exe"`  
(or set application path in environment variable and skip previous line)  
> `$ git config --global mergetool.meld.cmd 'meld "$LOCAL" "$MERGED" "$REMOTE" --output "$MERGED"'`  
> `$ git config --global mergetool.prompt true`  
If a conflict occurs during a merge it can be resolved graphically by, 
> `$ git mergetool`  

_**Colorful informative git**_  
>use posh-git for windows or zsh for unix


[Index][index]

[index]: ../index.md
