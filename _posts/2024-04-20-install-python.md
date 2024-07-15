---
layout: post
title: Install Python on Linux without Sudo
date: 2024-04-20 11:12:00-0400
description: 
tags: 
categories:
related_posts: false
---

I was running my machine learning project on a Linux server and needed to install Python 3.8 for some packages. I decided to install natively to keep everything under control, see this nice [blog](https://www.bitecode.dev/p/installing-python-the-bare-minimum). Without sudo right, things get a little different from standard installation but I found this nice [blog](https://www.bobbydurrettdba.com/2020/02/11/python-3-8-1-linux-install-without-root/) by Bobby Durrett making this super simple.


- Download the python from [www.python.org](https://www.python.org)

``` console
[hous@ada-25:Downloads] $ wget https://www.python.org/ftp/python/3.8.18/Python-3.8.18.tgz
Python-3.8.18.tgz   100%[===================>]  26.07M  --.-KB/s    in 0.1s    
2024-04-20 12:36:05 (230 MB/s) - ‘Python-3.8.18.tgz’ saved [27337549/27337549]
[hous@ada-25:Downloads] $ 
```
- Unzip it
- Go to the folder 

``` console
[hous@ada-25:Downloads] $ tar zxfv Python-3.8.18.tgz 
Python-3.8.18/
Python-3.8.18/Lib/
......
Python-3.8.18/config.guess
Python-3.8.18/Makefile.pre.in
[hous@ada-25:Downloads] $ cd Python-3.8.18/
[hous@ada-25:Python-3.8.18] $ 
```

- Check the absolute path of home directory
- Make a directory where you want to put your python. I called my <code>.localpython3.8</code> (name it whatever you want) and make it under the home directory.
- Configured the Python make 

``` console
[hous@ada-25:Python-3.8.18] $ pwd
/u/hous/Downloads/Python-3.8.18
[hous@ada-25:Python-3.8.18] $ mkdir /u/hous/.localpython3.8
[hous@ada-25:Python-3.8.18] $ ./configure --prefix=/u/hous/.localpython3.8
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
......
creating Modules/Setup.local
creating Makefile
If you want a release build with all stable optimizations active (PGO, etc),
please run ./configure --enable-optimizations
[hous@ada-25:Python-3.8.18] $ 
```

- Make and make altinstall (see difference between install and altinstall [here](https://stackoverflow.com/questions/16018463/difference-in-details-between-make-install-and-make-altinstall))

``` console
[hous@ada-25:Python-3.8.18] $ make
gcc -c -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall  
...
[hous@ada-25:Python-3.8.18] $ make altinstall
......
Successfully installed pip-23.0.1 setuptools-56.0.0
[hous@ada-25:Python-3.8.18] $ 
```

Now we can already use <code>~/.localpython3.8/bin/python3.8</code> to run python
``` console
[hous@ada-25:~] $ ~/.localpython3.8/bin/python3.8
Python 3.8.18 (default, Apr 20 2024, 12:51:15) 
[GCC 13.2.1 20240316 (Red Hat 13.2.1-7)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
[hous@ada-25:~] $ 
```
Perfect! Just to make life easier, we go to <code>~/.localpython3.8/bin/</code> and link <code>python3.8</code> to <code>python</code>
``` console
[hous@ada-25:Python-3.8.18] $ cd ~/.localpython3.8/bin
[hous@ada-25:bin] $ ln -s python3.8 python
[hous@ada-25:bin] $ ln -s pip3.8 pip
[hous@ada-25:bin] $ 
```
Now, we only need to type <code>~/.localpython3.8/bin/python</code>. Still a bit inconvenient, so next we add the folder path to PATH variable (abundant nice tutorial online explaining this). This is not just for convenient but avoid you running the wrong python.  

<code>export PATH=/u/hous/.localpython3.8/bin:$PATH</code> to <code>.bashrc</code> file.

``` console
[hous@ada-25:Python-3.8.18] $ cd ~
[hous@ada-25:~] $ vi .bashrc
# user's bashrc
#
export PATH=/u/hous/.localpython3.8/bin:$PATH
...
[hous@ada-25:~] $
```

After this, we logout and login. Now we can simply type <code>python</code> and check the installation.

``` console
[hous@ada-25:~] $ python
Python 3.8.18 (default, Apr 20 2024, 12:51:15) 
[GCC 13.2.1 20240316 (Red Hat 13.2.1-7)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
[hous@ada-25:~] $ pip -V
pip 23.0.1 from /u/hous/.localpython3.8/lib/python3.8/site-packages/pip (python 3.8)
[hous@ada-25:~] $ pip list
Package    Version
---------- -------
pip        23.0.1
setuptools 56.0.0

[notice] A new release of pip is available: 23.0.1 -> 24.0
[notice] To update, run: pip install --upgrade pip
[hous@ada-25:~] $ 
```

We are done! I usually then create a virtual environment and play with my machine learning codes, see [here](https://www.b-list.org/weblog/2022/may/13/boring-python-dependencies/) why venv is a good idea.




## Reference 
- [https://pages.github.nceas.ucsb.edu/NCEAS/Computing/local_install_python_on_a_server.html](https://pages.github.nceas.ucsb.edu/NCEAS/Computing/local_install_python_on_a_server.html)
- [https://www.bobbydurrettdba.com/2020/02/11/python-3-8-1-linux-install-without-root/](https://www.bobbydurrettdba.com/2020/02/11/python-3-8-1-linux-install-without-root/)
- [https://thelazylog.com/install-python-as-local-user-on-linux/](https://thelazylog.com/install-python-as-local-user-on-linux/)