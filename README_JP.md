# Character code Confirmation

## 概要
- 'path'に指定したファイルの文字コードを返却するパッケージ(モジュール)
- 'open()'を使用してファイルを開く際、指定する文字コートがわからない場合にこのモジュールが利用できます。
- 正確に文字コードを特定ものではないため、ファイルをオープンする際の'UnicodeDecodeError'を回避する方法として使用してください。

## インストール方法
- 任意のpythonのパッケージディレクトリにgetencodeを移動する
(pipでのインストールは現在できません)

## 使い方
### 確認する文字コードの指定をしない場合
- 指定したファイルを以下の文字コードで開くことができるか試し、結果を返却します。
- 'ascii euc-jp iso2022-jp iso2022_jp_2 shift_jis utf-8 utf_16_le cp932'
上記の文字コードに該当しない場合は、'None'を返却します。
```
from getencode import getenc

enc = getenc.getEncode(filePath)
```

### 確認する文字コードを指定する場合
- 独自で文字コードを指定する場合、文字コード一覧を引数に渡してください。
- 文字コードの間はスペースで区切ってください。
- 引数に使用できる文字コードの一覧は、getencode/getenc.pyにコメントで記述しています。
```
from getencode import getenc

origin = 'ascii shift_jis'

enc = getenc.getEncode(filePath, encType=origin)
```

## 例
- example/getenc.pyを実行すると、example/file/ディレクトリにあるファイルの文字コードをコマンドライン上で表示します。
```
cd getencode_package/example/
python3 getenc.py
```

## 具体例
- 複数のCSVファイルをオープンしたいが、それぞれの文字コートが異なる場合
```
import glob
import csv
from getencode import getenc

csvList = glob.glob('./*.csv')

for filePath in csvList:
    enc = getenc.getEncode(filePath)
        
    with open(filePath, 'r', encoding=enc) as f:
        data = csv.reader(f)
```

## その他
- 初めてのパッケージ作成/公開なので、プルリクエストお待ちしてます。
