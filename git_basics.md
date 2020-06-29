
# What is git

git is a distributed version control system that enables us to control versions of a project by tracking different versions of it
It generally keep track of all the commits (chunk of change) that we make to a project and lets us traverse through them and also move backward or forward at will.

Distributed version control system is different from Centralized version control system as DVCS allows user to have a updated copy of the whole repository and CVCS allows user to have only a version of the project.

# Primary git commands after installation

`>> git --version`\
*shows git version*

*set global config: username and email*\
`>> git config --global user.name <user_name>`\
`>> git config --global user.email <email>`

*all configuraiton list*\
`>> git config --list`\

*help/doc of any command*\
`>> git help <command_verb>`\
or\
`>> git <command_verb> --help`\

*ignore files*\
add files and wild-card entries to .gitignore file, files listed in it will be ignored by git.\
