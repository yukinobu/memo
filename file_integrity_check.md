# 破損ファイル検出

何らかの原因で破損したファイルを検出する方法のメモ。

以下は、カレントディレクトリ以下をスキャンして、破損分を表示するワンライナー。

## zip / Microsoft Office / jar / war

`zip` コマンドの `-T` オプションで確認。zip アーカイブとしての完全性検査なので、各アプリケーション独自の zip ファイルに対しては浅い検査に留まる。

```shell
find -type f -iname '*.zip' -o -iname '*.docx' -o -iname '*.xlsx' -o -iname '*.pptx' -o -iname '*.jar' -o -iname '*.war' | while read f; do zip -T "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

## pdf

poppler パッケージの`pdfinfo` コマンドで確認。おそらく、メタデータを中心に確認する浅い検査なので、ページの一部が破損しているようなケースは検出できないと思われる。

```shell
find -type f -iname '*.pdf' | while read f; do pdfinfo "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

参考資料

- https://superuser.com/questions/580887/check-if-pdf-files-are-corrupted-using-command-line-on-linux

## 画像系

ImageMagick の `identify` コマンドで確認。`-verbose` オプションをつけることで、画像の一部が破損したような場合でも検出できた。

```shell
find -type f -iname '*.jpg' -o -iname '*.png' -o -iname '*.gif' -o -iname '*.bmp' | while read f; do magick identify -verbose "${f}" >/dev/null 2>&1 || echo "${f}"; done
```

参考資料

- https://stackoverflow.com/questions/17757114/imagemagick-to-verify-image-integrity

## 動画系

VLC などでできないか調査中。

- https://stackoverflow.com/questions/30969307/convert-a-video-in-a-vlc-command-line#30980349
- https://wiki.videolan.org/VLC_command-line_help/
- https://wiki.videolan.org/Transcode

ffmpeg による方法があるようだが、手元ではうまく動いていない。

- https://superuser.com/questions/100288/how-can-i-check-the-integrity-of-a-video-file-avi-mpeg-mp4

