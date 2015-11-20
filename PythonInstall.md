
#Pythonの環境構築

　このテキストでは、Windows上でPythonの開発環境を構築するための方法を説明する。手っ取り早く環境を整えたい人は、**1,2,4,5節**を読んでいけばうまくいくはず。
  
##1.Python本体のインストール

　日本Pythonユーザー会にある [ダウンロードページ](http://www.python.jp/Zope/Zope/download/pythoncore)からダウンロード。64bitだとうまくいかない点があったので、32bit版を入手すること。また、最新バージョンは不安定な場合があるので少し古いバージョンの方がよい。ここではPython3.4を用いて説明をしていく。


###インストール時はパスの設定に注意 
　インストールは、インストーラの指示に従っていれば問題なく進められる。1点だけ気をつけないといけないのはパスの設定。インストール中の"Customize Python 3.4.0"のステップで"Add python.exe to Path"の項目の横にある×をクリックし、"will be installed on local hard drive"を選択すると、自動的にパスの設定が行われる。

　これを忘れると自分で入力してパスを設定する必要があるので少し面倒。そのときの手順は[こちら](http://www.pythonweb.jp/install/setup/index1.html)





##2.pipによる各種パッケージのインストール方法
　まず、Pythonのパッケージを簡単にダウンロードできるツールである**pip**を導入する必要がある。Python3.3ではpipを自動でインストールしてくれるので、バージョンアップのみ行えばOK。

　コマンドラインを管理者権限で立ち上げて（Windowsキー押す → cmdと入力 → CtrlとShift押しながらEnterキー）、

```
python -m pip install --upgrade pip
```

を入力すると、pipが最新版に更新される。
これ以降は次の1行でパッケージのインストールができる。

```
$ pip install <パッケージ名>
```

例) Numpyをインストールしたい場合は

```
$ pip install Numpy
```




##3.pipでインストールできない場合
（この節は読み飛ばしてもかまわない）


　原因不明だが、pipを使うとエラーが発生してインストールできないことがある。このときの対処法は主に次の2つ。
###方法I: 実行可能形式(.exe)のパッケージインストーラーを使う
　一部のパッケージには、Pythonのインストーラのようにexeファイルを実行することでパッケージのインストール作業を行ってくれるものもある。それを利用する方法。

###方法II: パッケージのバイナリをダウンロードして手動でインストール
　パッケージのバイナリファイル(拡張子.whlや.egg)をダウンロードして手動でインストールする方法。
パッケージは[こちら](http://www.lfd.uci.edu/~gohlke/pythonlibs/)のサイトなどでダウンロード可能。あるいは各パッケージの公式サイトから。
使っているPythonのバージョン、32/64bitに注意しながらパッケージを探し、ダウンロードする。
インストール方法は次の通り。まず管理者権限でコマンドラインを立ち上げる。
そして拡張子.whlの場合、

```
$ pip install --use-wheel --no-index --find-links=wheelhouse <パッケージ.whl>
```

拡張子.eggの場合、

```
$ easy_install <パッケージ.egg>
```

例) matplotlibのインストール  
Pythonの環境は次の通りとする。

- ver 3.5  
- 32bit 

ダウンロードしてくるのは"matplotlib‑1.5.0rc2‑cp35‑none‑win.whl"というファイル。これを適当なディレクトリに置き、次のコマンドを実行

```
$ pip install --use-wheel --no-index --find-links=wheelhouse matplotlib-1.4.3-cp35-none-win32.whl
```


  
  
##4.使うことになると思われるパッケージ
　研究のために以下のパッケージが必要になりそう

- Numpy
- Scipy
- matplotlib
- networkx


それぞれのインストール方法を順番に解説する。

　インストールされているパッケージの一覧は次のコマンドで確認可能なので、各パッケージをインストールするたびに確認しておくと安心。

```
$ pip freeze
```


###各パッケージのインストール方法

###・Numpy
　インストーラが用意されているので楽。
[このサイト](http://sourceforge.net/projects/numpy/files/NumPy/)で、バージョン1.10.1を選び"numpy-1.10.1-win32-superpack-python3.4.exe"をダウンロード。あとはインストーラを立ち上げて指示に従っていくだけ。

###・Scipy

　Numpyとほぼ同じ。[このサイト](http://sourceforge.net/projects/scipy/files/scipy/)で、バージョン0.16.0を選び"scipy-0.16.0-win32-superpack-python3.4.exe"をダウンロードし、インストーラを起動すればOK。

###・matplotlib
　これもNumpyとだいたい同じ。[こちら](http://sourceforge.net/projects/matplotlib/files/matplotlib/)からバージョン1.4.3を選び、"windows"の中にある"matplotlib-1.4.3.win32-py3.4.exe"をダウンロードし実行。ただしこれだけでは動作しない。matplotlibを動作させるために必要な次の３つのパッケージをインストールする。

--**six** 
--**pyparsing**  
　次のコマンドを実行すればOK

```
$ pip install six   
$ pip install pyparsing
```


--**dateutil**
　少し面倒。[こちら](https://pypi.python.org/pypi/python-dateutil)からバイナリをダウンロードし、次のコマンドを実行する。

```
$ pip install --use-wheel --no-index --find-links=wheelhouse python_dateutil-2.4.2-py2.py3-none-any.whl
```





###・networkx
　少し厄介。[ここ](https://pypi.python.org/pypi/networkx/)から"networkx-1.10-py3.4.egg"をダウンロードし、コマンドラインで次の命令を実行する

```
$ easy_install networkx-1.10-py3.4.egg
```


--------------------------------------------  
他にもパッケージを追加していく。  


##5.Eclipseの導入  
Pythonのコードを書きコンパイルするという一連の作業をするにはさまざまな方法があるが、WindowsではEclipseを使うと楽だと思われる。手順は次の通り。
###ダウンロード
まず[Eclipseのダウンロードサイト](http://mergedoc.osdn.jp/)でEclipseの最新版を選ぶ。（これを書いた時点では4.5)

