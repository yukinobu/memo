# 日常的なバックアップ

筆者がやっている日常的なバックアップ手法のいろいろ。

[[_TOC_]]

## コマンド

### rsync

Linux での標準は `rsync` コマンド。主に `ssh` 経由で遠隔バックアップする。以下は例。

```bash
rsync -avSz --delete -e ssh user@host:/etc/ /path_to_backup_of/etc/
```

```bash
rsync -e 'ssh -C' -avS --numeric-ids --bwlimit=256 --delete ./ user@host:/var/ /path_to_backup_of/var/
```

### robocopy

Windows での標準は `robocopy` コマンド。`start` コマンドを併用して低優先度で実行することが多い。以下は例。

```bat
start /B /LOW /WAIT C:\Windows\System32\Robocopy.exe %USERPROFILE% %~d0\userprofile /MIR /R:0 /XD AppData /XD Apple /XD node_modules /XD .mypy_cache
```

```bat
start /B /LOW /WAIT C:\Windows\System32\Robocopy.exe D:\photo %~d0\photo /MIR /R:0 /XF *.NEF /XF *.NRW /XF *.CR2 /XF *.DNG
```

コツとしては `/XD` や `/XF` オプションを使って、あまり余計なファイルをバックアップ対象にしないようにする。

### 7-zip

バックアップ時に圧縮や暗号化を併用したい場合、7-zip のコマンド `7z` が使用できる。以下は Windows での例。

```bat
"C:\Program Files\7-Zip\7z.exe" a -up1q0r2x1y2z1w2 -mx1 "E:\backup\backup.7z" "C:\path_to_backup\target"
```

`-up1q0r2x1y2z1w2` オプションは Synchronize モードの挙動。詳しくは: [-u (Update options) switch (osdn.jp)](https://sevenzip.osdn.jp/chm/cmdline/switches/update.htm)

また、日常的な実行には時間がかかりがちなので `-mx1` オプションで実行時間を短縮。詳しくは: [-m (Set compression Method) switch (osdn.jp)](https://sevenzip.osdn.jp/chm/cmdline/switches/method.htm#MultiThread)

### reg

Windows やアプリケーションの設定情報はレジストリに存在するので、`reg` コマンドでエクスポートして控えておく。

```bat
reg export "HKCU\SOFTWARE\SimonTatham\PuTTY" E:\backup\reg\PuTTY.reg /y
reg export "HKCU\SOFTWARE\RimArts\B2" E:\backup\reg\Becky2.reg /y
reg export "HKCU\Control Panel\Mouse" E:\backup\reg\mouse_setting.reg /y
```

