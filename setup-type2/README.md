howto-eclipse-setup : setup-type2
===============

setup-type2 対象:

- Eclipse 2018-12 R (4.10.2)
  - https://www.eclipse.org/eclipseide/
- Spring Tools 4 for Eclipse
  - https://spring.io/tools
- 4.10以降でも大体動くと思います。プラグインだけ対応度合いに差があるかもしれません。

※setup-type1と基本的に同様です。こちらでは差分だけ記述します。

## Eclipseのインストール

- Eclipse公式サイトの説明に従いインストールするか、手動でパッケージをダウンロードして展開する。
- Eclipseの実行に使うJDKをカスタマイズする例：
  1. eclipse.exe と同じフォルダにある eclipse.ini をコピーしてバックアップした後、eclipse.ini をエディタやメモ帳で開き、`-vmargs` の前に `-vm` + 改行 + JDKの `javaw.exe` までのフルパスを挿入する。
  1. 起動したら `Window` メニュー -> `Preferences` -> `[Java]` -> `[Installed JREs]` と辿り、eclipse.ini に挿入した `-vm` で指定したところのJDKの場所が認識されたことを確認する。(つまり、OSにインストールされてる "JRE" ではなく、きちんと自分がインストールした "JDK" を認識できていることを確認する)

`-vm` オプション挿入の実例:

```
...
--launcher.appendVmargs
-vmargs
-Dosgi.requiredJavaVersion=1.8
...
```

->

```
...
--launcher.appendVmargs
-vm
C:/work/devtools/jdk/adoptopenjdk-win-x64/jdk8u192-b12/bin/javaw.exe
-vmargs
-Dosgi.requiredJavaVersion=1.8
...
```

## おすすめプラグイン

- TODO : setup-type1との互換性を確認し、内容を更新。

## Workspaceのフォントや見た目のおすすめ設定

(setup-type1と同様)

## パースペクティブ(Perspective), ビュー(View)のおすすめ設定

(setup-type1と同様)

## GitやSubversionでチェックアウトしたMavenプロジェクトをインポートするには

(setup-type1と同様)

## Cleanup/Formatterのインポート

- setup-type1と同様の設定を入れた状態でXMLにエキスポートし、このREADME.mdと同じフォルダに同梱。
- Cleanup (Javaソースファイル保存時の自動処理) 設定のインポート:
  - `Window` メニュー -> `Preferences` -> `[Java]` -> `[Code Style]` -> `[Clean Up]` -> `[Import ...]` からインポートする。
- Formatter (Javaソースコードのフォーマッタ) 設定のインポート:
  - `Window` メニュー -> `Preferences` -> `[Java]` -> `[Code Style]` -> `[Formatter]` -> `[Import ...]` からインポートする。

## EGitからSSHでcloneするときの秘密鍵を指定するには

(setup-type1と同様)

