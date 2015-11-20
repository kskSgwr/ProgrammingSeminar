# Python の環境構築

Author: Keisuke Sugawara

Date: Oct. 9, 2015

OS: Windows

## Python 本体のインストール

　日本 Python ユーザー会にある[ダウンロードページ](http://www.python.jp/Zope/Zope/download/pythoncore)からダウンロード．64 bit だとうまくいかない点があったので，32 bit 版を入手すること．また，最新バージョンは不安定な場合があるので少し古いバージョンの方がよい．ここでは Python 3.4 を用いて説明をしていく．

* 注）インストール時のパスの設定 
  
  　インストールは ，インストーラの指示に従っていれば問題なく進められる．1 点だけ気をつけないといけないのはパスの設定．インストール中の Customize Python 3.4.0 のステップで Add python.exe to Path の項目の横にある × をクリックし，will be installed on local hard drive を選択すると，自動的にパスの設定が行われる．これを忘れると自分で入力してパスを設定する必要があるので少し面倒．そのときの手順は[こちら](http://www.pythonweb.jp/install/setup/index1.html)．

## パッケージのインストール

　まず，Python のパッケージを簡単にダウンロードできるツールである pip を導入する必要がある．Python 3.4 では pip を自動でインストールしてくれるので，バージョンアップのみ行えば OK．

　次に，コマンドラインを管理者権限で立ち上げて（Windows キー押す → cmd と入力 → Ctrl と Shift 押しながら Enter キー），`$ python -m pip install --upgrade pip` を入力すると，pip が最新版に更新される．これ以降は `$ pip install <packagename>` でパッケージのインストールができる．

　インストールされているパッケージの一覧は `$ pip freeze` で確認可能なので，各パッケージをインストールするたびに確認しておくと安心．

* 例）Numpy のインストール
  
  ```
  $ pip install numpy
  ```

### pip でインストールできない場合

　原因不明だが，pip を使うとエラーが発生してインストールできないことがある．このときの対処法は主に次の 2 つ．

#### 方法 I: 実行可能形式（.exe）のパッケージインストーラーを使う

　一部のパッケージには，Python のインストーラのように exe ファイルを実行することでパッケージのインストール作業を行ってくれるものもある．それを利用する方法．

#### 方法 II: パッケージのバイナリをダウンロードして手動でインストール

　パッケージのバイナリファイル（拡張子 .whl や .egg）をダウンロードして手動でインストールする方法．パッケージは[こちら](http://www.lfd.uci.edu/~gohlke/pythonlibs/)のサイトなどでダウンロード可能．あるいは各パッケージの公式サイトから．使っている Python のバージョン，32 / 64 bit に注意しながらパッケージを探し，ダウンロードする．

　インストール方法は次の通り．まず管理者権限でコマンドラインを立ち上げる．そして拡張子 .whl の場合，

```
$ pip install --use-wheel --no-index --find-links=wheelhouse <packagename>.whl
```

拡張子 .egg の場合，

```
$ easy_install <packagename>.egg
```

を実行．

* 例）matplotlib のインストール
  
  Python の環境は次の通りとする．

  * ver 3.5  
  * 32 bit 
  
  ダウンロードしてくるのは `matplotlib‑1.5.0rc2‑cp35‑none‑win.whl` というファイル．これを適当なディレクトリに置き，次を実行．
  
  ```
  $ pip install --use-wheel --no-index --find-links=wheelhouse matplotlib-1.4.3-cp35-none-win32.whl
  ```

### 主要なパッケージ

#### Numpy

　インストーラが用意されているので楽．[このサイト](http://sourceforge.net/projects/numpy/files/NumPy/)で，
バージョン 1.10.1 を選び `numpy-1.10.1-win32-superpack-python3.4.exe` をダウンロード．あとはインストーラを立ち上げて指示に従っていくだけ．

#### Scipy

　Numpy とほぼ同じ．[このサイト](http://sourceforge.net/projects/scipy/files/scipy/)で，バージョン 0.16.0 を選び `scipy-0.16.0-win32-superpack-python3.4.exe` をダウンロードし，インストーラを起動すれば OK．

#### matplotlib

　これも Numpy とだいたい同じ．[こちら](http://sourceforge.net/projects/matplotlib/files/matplotlib/)からバージョン 1.4.3 を選び，windows の中にある `matplotlib-1.4.3.win32-py3.4.exe` をダウンロードし実行．ただしこれだけでは動作しない．matplotlib を動作させるために必要な次の 3 つのパッケージをインストールする．

- six
- pyparsing
  
  次を実行すればOK．
  
  ```
  $ pip install six
  $ pip install pyparsing
  ```

- dateutil
  
  少し面倒．[こちら](https://pypi.python.org/pypi/python-dateutil)からバイナリをダウンロードし，`$ pip install --use-wheel --no-index --find-links=wheelhouse python_dateutil-2.4.2-py2.py3-none-any.whl` を実行する．

#### networkx

　少し厄介．[ここ](https://pypi.python.org/pypi/networkx/)から `networkx-1.10-py3.4.egg` をダウンロードし， `$ easy_install networkx-1.10-py3.4.egg` を実行する．
