# 破損ファイル検出

何らかの原因で破損したファイルを検出する方法のメモ。

以下は、カレントディレクトリ以下をスキャンして、破損分を表示するワンライナー。

## zip / Microsoft Office / jar / war

`zip` コマンドの `-T` オプションで確認。zip アーカイブとしての完全性検査なので、各アプリケーション独自の zip ファイルに対しては浅い検査に留まる。

```shell
find -type f \( -iname '*.zip' -o -iname '*.docx' -o -iname '*.xlsx' -o -iname '*.pptx' -o -iname '*.jar' -o -iname '*.war' \) | while read f; do zip -T "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

## pdf

poppler パッケージの `pdfinfo` コマンドで確認。おそらく、メタデータを中心に確認する浅い検査なので、ページの一部が破損しているようなケースは検出できないと思われる。

```shell
find -type f -iname '*.pdf' | while read f; do pdfinfo "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

参考資料

- https://superuser.com/questions/580887/check-if-pdf-files-are-corrupted-using-command-line-on-linux

## 画像系

ImageMagick の `identify` コマンドで確認。`-verbose` オプションをつけることで、画像の一部が破損したような場合でも検出できた。

```shell
find -type f \( -iname '*.jpg' -o -iname '*.png' -o -iname '*.gif' -o -iname '*.bmp' \) | while read f; do magick identify -verbose "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

参考資料

- https://stackoverflow.com/questions/17757114/imagemagick-to-verify-image-integrity

## Nikon RAW画像

`exiftool` コマンドを使用して Image Size を取得できなければ破損していると判断。浅い検査なので、途中の一部が破損しているようなケースは検出できない。

```shell
find -type f \( -iname '*.nef' -o -iname '*.nrw' \) | while read f; do test `exiftool "${f}" | grep -E '^Image Size' | wc -l` -gt 0 || echo "${f}"; done
```

参考資料

- https://sno.phy.queensu.ca/~phil/exiftool/

## 動画系

MediaInfo の CLI 版を利用し、Duration が取得できなければ破損していると判断。浅い検査なので、途中の一部が破損しているようなケースは検出できない。

```shell
find -type f \( -iname '*.avi' -o -iname '*.wmv' -o -iname '*.mpg' -o -iname '*.mp4' -o -iname '*.m4v' -o -iname '*.mkv' -o -iname '*.mov' -o -iname '*.rm' \) | while read f; do test `MediaInfo "${f}" | grep -E '^Duration' | wc -l` -gt 0 || echo "${f}"; done
```

参考資料

- https://mediaarea.net/en/MediaInfo