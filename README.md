# pyenv-setup

https://qiita.com/saitou1978/items/e82421e29e118bd397cc 
を参考

## 事前準備

### 使用可能なversion確認
```
pyenv install -l
```

### インストール
ひとまず使いそうな2.7系と3.5系をインストール済
```
❯ pyenv install 2.7.15
Downloading Python-2.7.15.tar.xz...
-> https://www.python.org/ftp/python/2.7.15/Python-2.7.15.tar.xz
Installing Python-2.7.15...
Installed Python-2.7.15 to /home/vagrant/.pyenv/versions/2.7.15


~ localhost.localdomain 2m 2s
❯ pyenv install 3.5.6
Downloading Python-3.5.6.tar.xz...
-> https://www.python.org/ftp/python/3.5.6/Python-3.5.6.tar.xz
Installing Python-3.5.6...
Installed Python-3.5.6 to /home/vagrant/.pyenv/versions/3.5.6
```

```
❯ pyenv versions
* system (set by /home/vagrant/.pyenv/version)
  2.7.15
  3.5.6
```

### version変更
```
❯ pyenv global 2.7.15

~ localhost.localdomain
❯ python --version
Python 2.7.5

~ localhost.localdomain
❯ exec zsh -l

~ localhost.localdomain
❯ python --version
Python 2.7.15
```

## 新環境構築

2.7.15で複製環境から独立した環境を作成できる

```
❯ pyenv virtualenv 2.7.15 py27
Collecting virtualenv
  Cache entry deserialization failed, entry ignored
  Downloading https://files.pythonhosted.org/packages/8f/f1/c0b069ca6cb44f9681715232e6d3d65c75866dd231c5e4a88e80a46634bb/virtualenv-16.3.0-py2.py3-none-any.whl (2.0MB)
    100% |████████████████████████████████| 2.0MB 600kB/s
Requirement already satisfied: setuptools>=18.0.0 in /home/vagrant/.pyenv/versions/2.7.15/lib/python2.7/site-packages (from virtualenv)
Installing collected packages: virtualenv
Successfully installed virtualenv-16.3.0
You are using pip version 9.0.3, however version 19.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
New python executable in /home/vagrant/.pyenv/versions/2.7.15/envs/py27/bin/python2.7
Also creating executable in /home/vagrant/.pyenv/versions/2.7.15/envs/py27/bin/python
Installing setuptools, pip, wheel...
done.
Requirement already satisfied: setuptools in /home/vagrant/.pyenv/versions/2.7.15/envs/py27/lib/python2.7/site-packages
Requirement already satisfied: pip in /home/vagrant/.pyenv/versions/2.7.15/envs/py27/lib/python2.7/site-packages

```

### repo作成
作業ディレクトを作成
```
❯ mkdir py-foo

~ localhost.localdomain
❯ cd py-foo
```

使用する環境をlocalに適用
```
~/py-foo localhost.localdomain
❯ pyenv local py27
```

.python-versionファイルができる
```
~/py-foo localhost.localdomain
py27 ❯ la
total 4.0K
-rw-rw-r--. 1 vagrant vagrant 5 Jan 29 11:49 .python-version
```

```
~/py-foo localhost.localdomain
py27 ❯ pip list
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won't be maintained after that date. A future version of pip will drop support for Python 2.7.
Package    Version
---------- -------
pip        19.0.1
setuptools 40.7.1
wheel      0.32.3
```

## 環境削除
```
❯ pyenv versions
  system
* 2.7.15 (set by /home/vagrant/.pyenv/version)
  2.7.15/envs/py27
  3.5.6
  3.5.6/envs/py35
  py27
  py35

~ localhost.localdomain
❯ pyenv uninstall py35
pyenv-virtualenv: remove /home/vagrant/.pyenv/versions/3.5.6/envs/py35? y

~ localhost.localdomain
❯ pyenv versions
  system
* 2.7.15 (set by /home/vagrant/.pyenv/version)
  2.7.15/envs/py27
  3.5.6
  py27

```
