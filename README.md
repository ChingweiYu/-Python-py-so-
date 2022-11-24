# -Python-py-so-
1. 緣由

Python的解釋特性是將py編譯為獨有的二進位制編碼pyc檔案
然後對pyc中的指令進行解釋執行
但是pyc的反編譯卻非常簡單，可直接反編譯為原始碼
正所謂「防人之心不可無」
當需要將產品釋出到外部環境的時候，原始碼的保護尤為重要
2. 辦法

可以先將py轉換為c，然後編譯c為so檔案
2.1. 軟體環境

安裝 cython

$ pip3 install cython

2.2. 原始檔

在py_to_so資料夾下新建test.py檔案待編譯，內容如下：

class TEST:
    def hello():
        print('Hello CSDN!')

2.3. setup.py

在py_to_so資料夾下新建setup.py檔案，內容如下：

from distutils.core import setup
from Cython.Build import cythonize

setup(ext_modules = cythonize(["test.py"]))

2.4. 執行編譯

在py_to_so資料夾下執行編譯

$ python3 setup.py build_ext

在這裡插入圖片描述
執行後會生成build資料夾，如下：
在這裡插入圖片描述

lib.linux-x86_64-3.8資料夾下的test.cpython-38-x86_64-linux-gnu.so就是想要的.so檔案

在這裡插入圖片描述
2.5. 使用

現在so檔案就可以像普通py檔案一樣匯入使用

$ cd build/lib.linux-x86_64-3.8
$ python3
$ from test import TEST
$ TEST.hello()
# Hello CSDN!

在這裡插入圖片描述
2.6. inplace

$ python3 setup.py build_ext --inplace

–inplace：ignore build-lib and put compiled extensions into the source directory alongside your pure Python modules
忽略build-lib，將編譯後的擴充套件放到源目錄中，與Python模組放在一起
在這裡插入圖片描述
