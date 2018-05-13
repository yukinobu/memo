# 破損ファイル検出

何らかの原因で破損したファイルを検出したい。

以下は、カレントディレクトリ以下をスキャンして、破損分を表示するワンライナー。

### zip / Microsoft Office / jar / war

`zip` コマンドの `-T` オプションで確認する。zip アーカイブとしての完全性検査なので、各アプリケーション独自の zip ファイルに対しては浅い検査に留まる。

```shell
find -type f -iname '*.zip' -o -iname '*.docx' -o -iname '*.xlsx' -o -iname '*.pptx' -o -iname '*.jar' -o -iname '*.war' | while read f; do zip -T "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

### pdf

poppler パッケージの`pdfinfo` コマンドで確認する。おそらく、メタデータを中心に確認する浅い検査なので、ページの一部が破損しているようなケースは検出できないと思われる。

```shell
find -type f -iname '*.pdf' | while read f; do pdfinfo "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

## 画像系

ImageMagick の `identify` コマンドで確認。おそらく、メタデータを中心に確認する浅い検査なので、画像の一部が破損しているようなケースは検出できないと思われる。

```shell
find -type f -iname '*.jpg' -o -iname '*.png' -o -iname '*.gif' -o -iname '*.bmp' | while read f; do magick identify "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

### 動画系

VLC などでできないか調査中。