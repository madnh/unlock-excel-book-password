# Unlock Excel Book Password

読み取り専用パスワードがかけられた Excel ブックを総当たりで開こうとする VBScript です。

## 使い方

- `Unlock.bat` 経由で `Unlock.vbs` を起動して使ってください。
- 設定ファイル `Property.txt` に開きたいブックなどの情報を記載してください。
- パスワードが解除できると、`Unlocked.txt` にパスワードを書き込みます。

## `Property.txt` の書き方

- `[プロパティ名]=[値]` の形式で記述します。イコール `=` の前後にスペースは付けないでください。
- `fileName=` : 開きたいブック名をフルパスで書きます。  
例 : `fileName=P:\UnlockExcelBookPassword\Sample.xlsx`
- `min=` : 探索するパスワード長の最小桁を指定します。  
例 : `min=4` (4桁の組み合わせから始める)
- `max=` : 探索するパスワード長の最大桁を指定します。  
例 : `max=6` (6桁の組み合わせまで探索する)
- `strings=` : 探索に使用する文字列をスペースなしカンマ区切りで指定します。  
例 : `strings=0,1,2,3,4,5,6,7,8,9`
- `progressStr=` : 最後に探索した文字列を指定しておくと、次回起動時にこの文字列からレジュームして探索を再開します。任意設定項目なので、不要なら `progressStr=` と空にしておいてください。  
例 : `progressStr=00200` (`00200` という文字列から探索を再開する)

### `strings` プロパティについて

探索に使用する文字列を指定できます。「`hoge` と `fuga` という文字列の組み合わせでパスワードを作ったと思うんだけど…」というように、ある程度使用している文字が推測できている場合は、

```
strings=h,o,g,e,f,u,a
```

というように指定すれば、これらの文字から総当たりで組み合わせの文字列を作成します。数字やその他のアルファベットなどが対象にならないので、探索時間を短縮できます。

### `progressStr` プロパティについて

探索処理を再開するときにレジュームさせるための項目です。

例えば対象のパスワードが `00201` だったとして、数字のみの組み合わせで3桁目から探索しようとした場合は、以下のような設定項目で始めます。

```
min=3
max=6
strings=0,1,2,3,4,5,6,7,8,9
progressStr=
```

この状態でスクリプトを起動して探索を始めたものの、`0900` の組み合わせ文字列を試したところでスクリプトを中断させたとします。その時は、設定ファイルを

```
progressStr=0900
```

と書き換えてスクリプトを起動することで、次回は `0901` からの組み合わせ文字列で探索を再開できます。3文字の場合の組み合わせはスキップし、4文字の場合の組み合わせも `0000` ～ `0900` までの組み合わせをスキップできます。

再起動するタイミングで `strings` プロパティは変えないようにしてください。正常にレジュームできなくなります。

## サンプルファイルについて

`Sample.xlsx` は `00201` で開けるサンプルファイルです。中身は何もありませんし、スクリプト動作に必要なファイルでもありません。

同梱の `Property.txt` はこの `Sample.xlsx` を開くテイで記述しています。`fileName=` 部分のフルパスを各自の環境に合わせて修正して試してみてください。

## Special Thanks

一方的に以下のスクリプトを参考にさせていただきました。

- [エクセルパスワード解除 VB スクリプト](https://gist.github.com/toagit/b83d6fb3670045745caa)
- [Excel のパスワード解除 (VBS 版)](http://n73.jugem.jp/?eid=22)
    - 大枠はこちらのスクリプトを利用したものです。
- [Excel UnPassword](http://www.acchi.cc/soft/eup/index.html)
    - レジュームのアイデアを拝借しました。


## Author

[Neo](http://neo.s21.xrea.com/) ([@Neos21](https://twitter.com/Neos21))


## Links

- [Neo's World](http://neo.s21.xrea.com/)
- [Corredor](http://neos21.hatenablog.com/)
- [Murga](http://neos21.hatenablog.jp/)
- [El Mylar](http://neos21.hateblo.jp/)
- [Bit-Archer](http://bit-archer.hatenablog.com/)
- [GitHub - Neos21](https://github.com/Neos21/)
