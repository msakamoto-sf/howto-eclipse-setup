howto-eclipse-setup : setup-type1
===============

setup-type1 対象:

- Eclipse Mars.2 Release (4.5.2)
- 4.6以降でも大体動くと思います。プラグインだけ対応度合いに差があるかもしれません。

## Eclipseのインストール

良くある落とし穴:

1. EclipseのzipをWindowsで展開したとき、展開先のパス名が長くなり、プラグインフォルダ・ファイル名などでパス名の長さ制限を超えてしまい、一部で展開が失敗する。
  - パス名が短くなるよう、なるべくドライブから浅いフォルダに展開するようにする。
1. JDKではなく、 https://java.com/ja/ からインストールしたJREだけで動かしてしまうことにより、JDK依存機能が使えない / JRE側の自動更新による予期せぬ副作用でトラブル。
  - 必ず手動でJDKを入れて、 eclipse.ini の `-vm` オプションで使用する `javaw.exe` を明示的に指定する。

おすすめ手順:

1. http://www.oracle.com/technetwork/java/javase/downloads/index.html よりJDKをインストール
1. https://www.eclipse.org/downloads/packages/release/Mars/2 より「Eclipse IDE for Java EE Developers」(64bit)をダウンロード
1. ダウンロードしたらzipを展開するが、なるべくパス名が短くなるようにする。(プラグインフォルダ・ファイル名などでWindowsのパス名の長さ制限を超える場合があるため、フォルダを深く掘った先に展開しないよう注意。展開時にエラーが出たら、より短いパス名になるよう、フォルダ階層を上にずらすこと)
1. eclipse.exeと同じフォルダにある eclipse.ini をコピーしてバックアップした後、eclipse.ini をエディタやメモ帳で開く。
1. `-vmargs` の前に、`-vm` + 改行 + JDKの `javaw.exe` までのフルパスを挿入する。
1. eclipse.exeを起動する。
1. 起動したら `Window` メニュー -> `Preferences` -> `[Java]` -> `[Installed JREs]` と辿り、eclipse.ini に挿入した `-vm` で指定したところのJDKの場所が認識されたことを確認する。(つまり、OSにインストールされてる "JRE" ではなく、きちんと自分がインストールした "JDK" を認識できていることを確認する)

`-vm` オプション挿入の実例:

```
...
--launcher.appendVmargs
-vmargs
-Dosgi.requiredJavaVersion=1.7
...
```

->

```
...
--launcher.appendVmargs
-vm
C:/work/devtools/jdk/jdk1.8.0_92/bin/javaw.exe
-vmargs
-Dosgi.requiredJavaVersion=1.7
...
```

## おすすめプラグイン

- Eclipse Mars 2 の Java EE Developers 向けのパッケージングですと EGit, m2e, m2e-wtp が同梱されていますので、Gitでアクセスする一般的なMavenプロジェクトであればそのままインポート可能です。
- その他のおすすめプラグインについては開発内容によって変わりますが、こちらの setup-type1 を使っている開発プロジェクトでは追加で以下のようなプラグインを使っていたりします。


- `TestNG`, `TestNG M2E Integration(Optional)`
  - JUnit と同等の、Javaの単体テストライブラリ TestNG をEclipse上から実行できるプラグイン。
  - 一部の開発プロジェクトでは JUnit ではなく TestNG を使ってるので、使ってます。
  - Eclipse Marketplace から `TestNG` で検索、`TestNG for Eclipse` をデフォルト選択でインストール。
- `FindBugs Eclipse Plugin`
  - Eclipse Marketplace から `FindBugs` で検索、デフォルト選択でインストール。
- `Checkstyle Plugin`
  - Eclipse Marketplace から `Checkstyle` で検索、デフォルト選択でインストール。
- `ERMaster`
  - http://ermaster.sourceforge.net/index_ja.html
- `Groovy Eclipse Plugin`
  - https://github.com/groovy/groovy-eclipse/wiki 参照してインストール。
  - 使用するアップデートサイト : http://dist.springsource.org/snapshot/GRECLIPSE/e4.5/
    1. `Help` => `Install New Software...` => `Work with: ` にURLを入力し "Add"ボタンクリック。
    1. "Add Repository" で Name に "`Groovy Eclipse e4.5`" と入力してOKボタンクリック。
    1. チェックを入れてインストールする項目：
       - `Groovy Compiler 2.3 Feature` (こちらを使用しているプロジェクトでは、2.3以降を使用)
       - `Groovy-Eclipse Feature`
       - `Groovy-Eclipse M2E integration`
       - `JDT Core patch for Groovy-Eclipse plugin on Eclipse 4.5`

## Workspaceのフォントや見た目のおすすめ設定

`Window` メニュー -> `Preferences` から:

- フォントのカスタマイズ：
  - `[General]` -> `[Appearance]` -> `[Colors and Fonts]` -> `Basic` -> `Text Font` : お好みの等幅フォントに変更。ソースコードエディタ・コンソールViewなどに表示するフォントになる。
- 行番号と空白文字の表示
  - `[General]` -> `[Editors]` -> `[Text Editors]` -> `Show line numbers` と `Show whitespace characters` にチェックを入れる。
- ファイルセーブ時に使ってない import 文を消す
  - `[Java]` -> `[Editor]` -> `[Save Actions]` -> `Perform the selected actions on save` にチェックを入れ、`Organize imports` にチェックを入れる。
- 補完時に上書きする
  - `[Java]` -> `[Editor]` -> `[Content Assist]` -> `Complletion overwrites` にチェックを入れる。
- assertThat とか補完できるようにする(JUnit版)
  - `[Java]` -> `[Editor]` -> `[Content Assist]` -> `[Favorites]` に `org.junit.Assert` と `org.hamcrest.CoreMatchers` を追加
- assertEquals とか補完できるようにする(TestNG版)
  - `[Java]` -> `[Editor]` -> `[Content Assist]` -> `[Favorites]` に `org.testng.Assert` を追加
- どこで「;」を押しても行末にいれる
  - `[Java]` -> `[Editor]` -> `[Typing]` -> `Automatically insert at correct position` の `Semicolons` にチェックを入れる。
- クラス名なのか変数名なのかわかりやすくするためのSyntax Coloring
  - `[Java]` -> `[Editor]` -> `[Syntax Coloring]` -> Classes,Enums,IntefacesをEnable,Boldにする。
- java.awt.ListとかSwingパッケージを補完対象から外す
  - `[Java]` -> `[Appearance]` -> `[Type Filters]` -> `java.awt.*`, `javax.swing.*` を追加
- Workspaceでの改行コードや文字コード
  - `[General]` -> `[Workspace]` で変更。（最近はデフォルトでUTF-8になってる。改行もデフォルト任せでよい）
- JSPファイルの文字コード
  - `[General]` -> `[Content Types]` で"Text" - "JSP"のDefault encodingをUTF-8に変更
  - `[Web]` -> `[JSP Files]` でEncodingを設定 (Mars.2だとデフォルトでUTF-8になってた)

## パースペクティブ(Perspective), ビュー(View)のおすすめ設定

パースペクティブ(Perspective):

- `Java EE` は使わなければcloseしてOK.(機能が豊富だが、使わない機能が多ければ `Java` パースペクティブで十分)
- `Window` -> `Perspective` -> `Open Perspective` から以下のパースペクティブをOpenしておくのがおすすめ。
  - `Java`, `Debug`, `Git`

`Java` パースペクティブで必須のView : `Window` -> `Show View` -> `Other...` から表示できる。

- `Package Explorer`
  - プロジェクト内の論理的なエクスプローラ。Eclipseプロジェクトの設定ファイルなど非表示。
- `Navigator`
  - プロジェクトファイル全てのエクスプローラ。Eclipseプロジェクトの設定ファイルなども表示。
- `Outline`
  - 開いたファイルの論理構成アウトラインを表示。Java, XMLなどに対応。
- `Type Hierarchy`
  - Javaソースのクラス継承の階層構造を表示。
- `Problems`
  - コンパイルエラーや警告、その他のエラーなど表示。
- `Console`
  - Java/Groovy/Tomcat実行時の標準入出力, エラー出力
- `Progress`
  - workspaceやプロジェクトのビルドなど様々な処理の進捗状況を表示。これがないと、裏側で何が行われているのか分からなくなる。
- `Tasks`
  - `TODO` などでマークした箇所を一覧表示。
- `Error Log`
  - Eclipse 自体の実行時のエラーや警告、情報ログなどが表示される。
- `Servers`
  - Webアプリ(Servletなど)実行時に使うサーバ設定を登録・表示。
- `Checkstyle violations`
  - Checkstyle の検出結果を表示。(Checkstyleを使う場合は有用)
- `Bug Explorer`
  - FindBugs の検出結果を表示。(FindBugsを使う場合は有用)
- `Search`
  - 検索結果を表示。
- `TestNG`
  - `TestNG` 実行結果を表示。

## Cleanup/Formatterのインポート

- Cleanup (Javaソースファイル保存時の自動処理) 設定のインポート:
  - `Window` メニュー -> `Preferences` -> `[Java]` -> `[Code Style]` -> `[Clean Up]` -> `[Import ...]` からインポートする。
- Formatter (Javaソースコードのフォーマッタ) 設定のインポート:
  - `Window` メニュー -> `Preferences` -> `[Java]` -> `[Code Style]` -> `[Formatter]` -> `[Import ...]` からインポートする。

## EGitからSSHでcloneするときの秘密鍵を指定するには

https://wiki.eclipse.org/EGit/User_Guide/Remote より, `Windows` メニュー -> `Preferences` -> `[General]` -> `[Network Connections]` -> `[SSH2]` で、以下の項目をチェック。

- "General" タブで、"SSH2 Home" は適切か？
- "General" タブで、"Private keys" は適切な秘密鍵ファイル名が設定されているか？
- "Key Management" タブで、 "Load Existing Key..." で秘密鍵の読み込みは試したか？
- "Authentication Methos" タブで、"password" のチェックを外したか？（外してなければ、外す）

なおこちらで扱えるのは OpenSSH 系のツールで生成した秘密鍵。putty系やWinSCP系のツールで生成した秘密鍵はそのままでは扱えないので、OpenSSH系にエクスポートしたものを使用するよう注意が必要。

