# about

本レポジトリ https://github.com/fushihara/python-arib は https://github.com/johnoneil/arib をフォークした物です。レポジトリ名が変更されている点にご注意ください。

windows10 64bit Pro、python 2.7(anaconda)、powershell(コンソールの文字コードがsjisとutf8、つまりchcp 65001とchcp 932)で動作確認をしています。
日本語ファイル名での動作確認をしています。

上記の環境で動作させる為にオリジナルのコードから変更が発生しています。


## 使い方

セットアップ方法はオリジナルと同じです。

```
git clone https://github.com/fushihara/python-arib .
pip install -e .
```

インストール後使えるようになるコマンドの説明


- `arib-ts2ass "C:\test\テスト.ts"`
tsと同じフォルダにassファイルを作成します。 `"C:\test\テスト.ts.ass"`

assファイルの中身一部

```
[Script Info]
; *****************************************************************************
; File generated via arib-ts2ass
; https://github.com/johnoneil/arib
; *****************************************************************************
Title: Japanese Closed Caption Subtitlies
ScriptType: v4.00+
WrapStyle: 0
PlayResX: 960
PlayResY: 540
ScaledBorderAndShadow: yes
Video Aspect Ratio: 0
Video Zoom: 1
Video Position: 0
Last Style Storage: Default
Video File: C:\test\テスト.ts.ass


[V4+ Styles]
Format: Name, Fontname, Fontsize, PrimaryColour, SecondaryColour, OutlineColour, BackColour, Bold, Italic, Underline, StrikeOut, ScaleX, ScaleY, Spacing, Angle, BorderStyle, Outline, Shadow, Alignment, MarginL, MarginR, MarginV, Encoding
Style: normal,MS UI Gothic,37,&H00FFFFFF,&H000000FF,&H00000000,&H88000000,0,0,0,0,100,100,0,0,1,2,2,1,10,10,10,0
Style: medium,MS UI Gothic,37,&H00FFFFFF,&H000000FF,&H00000000,&H88000000,0,0,0,0,50,100,0,0,1,2,2,1,10,10,10,0
Style: small,MS UI Gothic,18,&H00FFFFFF,&H000000FF,&H00000000,&H88000000,0,0,0,0,100,100,0,0,1,2,2,1,10,10,10,0


Dialogue: 0,0:00:55.12,0:00:57.03,normal,,0000,0000,0000,,{\rnormal}{\c&Hffffff&}{\pos(170,510)}{\c&Hffffff&}ふう…\N
Dialogue: 0,0:00:57.03,0:00:59.08,normal,,0000,0000,0000,,{\rnormal}{\c&Hffffff&}{\pos(170,510)}{\c&Hffffff&}うん\N
Dialogue: 0,0:00:59.08,0:01:2.05,normal,,0000,0000,0000,,{\rnormal}{\c&Hffffff&}{\pos(170,510)}{\c&Hffffff&}今日{\rmedium}{\c&Hffffff&}　{\rnormal}{\c&Hffffff&}才川と公園で遊ぶ約束した\N

```

- `arib-ts-extract "C:\test\テスト.ts"`
標準出力に詳細な情報を出力します。恐らく、TSに保存されている字幕の生データです

```
> arib-ts-extract "C:\test\テスト.ts"
Closed caption management data for language: jpn available in PID: 4622
Will now only process this PID to improve performance.
File elapsed time seconds: 55.1174111111
<clear screen>
File elapsed time seconds: 55.1174111111
<CS:"7 S"><CS:"620;480 V"><CS:"170;30 _"><CS:"4 X"><CS:"24 Y"><CS:"36;36 W"><CS:"8 n"><CS:"1;0000 c">
<Screen Posiiton to 7,0><white>ふう…
File elapsed time seconds: 57.0316777778
<clear screen>
File elapsed time seconds: 57.0316777778
<CS:"7 S"><CS:"620;480 V"><CS:"170;30 _"><CS:"4 X"><CS:"24 Y"><CS:"36;36 W"><CS:"8 n"><CS:"1;0000 c">
<Screen Posiiton to 7,0><white>うん
File elapsed time seconds: 59.0779222222
<clear screen>
File elapsed time seconds: 59.0779222222
<CS:"7 S"><CS:"620;480 V"><CS:"170;30 _"><CS:"4 X"><CS:"24 Y"><CS:"36;36 W"><CS:"8 n"><CS:"1;0000 c">
<Screen Posiiton to 7,0><white>今日<Medium Text>　<Normal Text>才川と公園で遊ぶ約束した
File elapsed time seconds: 62.0483666667
<clear screen>
File elapsed time seconds: 62.0483666667
```

- `arib-es-extract`
動作確認が出来ませんでした。以下の内容より先頭のバイナリが0x80でないというエラーの様だが、TSであれば先頭は0x47であるはず。es-extractなのでtsを引数に指定する事がおかしいのかも？

```
> arib-es-extract "C:\test\テスト.ts"
Exception throw while parsing data group from .es
Traceback (most recent call last):
  File "c:\xxx\python-arib-fork\arib\data_group.py", line 131, in next_data_group
    data_group = DataGroup(f)
  File "c:\xxx\python-arib-fork\arib\data_group.py", line 54, in __init__
    raise DataGroupParseError("Initial stuffing byte not equal to 0x80: " + hex(self._stuffing_byte))
DataGroupParseError: Initial stuffing byte not equal to 0x80: 0x47
```
