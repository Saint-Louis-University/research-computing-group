---
date: "2019-01-25"
title: "Multiple Versions of Python"
type: post
---

There are a few reasons you may need a different version of Python. You may need a newer version of Python or need multiple modules installed. This can be accomplished with pyenv.

This can be installed in your /home directory by following the instructions below.

1.&nbsp;&nbsp;Cut and paste the following code to your command prompt.

    curl -L https://raw.github.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash

2.&nbsp;&nbsp;Add the code listed below to your .bashrc file. Type nano .bashrc to edit the file. Then paste the following code at the end of 
   the file.

    export PYENV_ROOT="${HOME}/.pyenv"

    if [ -d "${PYENV_ROOT}" ]; then
     export PATH="${PYENV_ROOT}/bin:${PATH}"
     eval "$(pyenv init -)"
    fi

3.&nbsp;&nbsp;Then press the ctrl-x keys together to save the file.

4.&nbsp;&nbsp;Type the following.

    source ~/.bash_profile

5.&nbsp;&nbsp;To see a list of the available versions of python type the following.
 
    pyenv install -l

6.&nbsp;&nbsp;To install a Python version type the following.

    pyenv install <version>

<u>[Pyenv Documentation](https://github.com/pyenv/pyenv)</u>