# AtsExCsTemplate
AtsEXを使ったBve5またはBve6用プラグインのテンプレート


## ライセンス
[MIT](LICENSE)


## このテンプレートの機能
- 取っ掛かりやすいように3種類のプラグインのファイル
    - マッププラグイン
    - 車両プラグイン
    - 拡張機能
- コードチェック
- ciでのdll自動生成


## 動作環境
- [AtsEX](https://github.com/automatic9045/AtsEX)
    - [ver1.0-RC3 - v1.0.31118.2](https://github.com/automatic9045/AtsEX/releases/tag/v1.0.31118.2)
- Win10 22H2(更新してないけど23H2でも動くはず)
    - Visual Studio 2022
        - Microsoft Visual Studio Community 2022 (64 ビット) - Current Version 17.5.3
- [Bve](https://bvets.net/)
    - BVE Trainsim Version 6.0.7554.619


## 依存環境
- AtsEx.CoreExtensions (0.19.0)
    - AtsEx.PluginHost (>= 1.0.0-rc1)
        - Lib.Harmony (>= 2.2.2)
        - SlimDX (>= 4.0.13.44)
        - UnembeddedResources (>= 1.0.0)
    - ObjectiveHarmonyPatch (>= 1.0.0)
        - Lib.Harmony (>= 2.2.2)


[AtsEX](https://github.com/automatic9045/AtsEX)
    - [ver1.0-RC3 - v1.0.31118.2](https://github.com/automatic9045/AtsEX/releases/tag/v1.0.31118.2)
- Win10 22H2(更新してないけど23H2でも動くはず)
    - Visual Studio 2022
        - Microsoft Visual Studio Community 2022 (64 ビット) - Current Version 17.5.3
- [Bve](https://bvets.net/)
    - BVE Trainsim Version 6.0.7554.619


## 使い方
1. Use this template から新しくリポジトリを作成する
1. 自分の作りたい機能に合わせて設定する
1. コードを書く
1. リリースする

### 0. 下準備
#### 0.1. Visual Studio でビルドできる状態にする
1. AtsExCsTemplate.csproj を開いてすべて保存から適当な場所にslnを生成する
1. NuGetからAtsEx関連のライブラリを入れる（ビルドすれば勝手に入る）
1. 開発するプラグインの種類に応じて要らないファイルを削除する
    - MapPlugin.cs
        - マッププラグイン用のソースコード
    - VehiclePlugin.cs
        - 車両プラグイン用のソースコード
    - Extension.cs
        - 拡張機能用のソースコード

#### 0.2. プラグイン情報の設定
**Properties/AssemblyInfo.cs**
BveからAtsExのバージョン情報を見たときに表示される内容を設定できます
AtsExのバージョン情報画面から見えるのはファイル名と下の3項目です

- AssemblyTitle
    - プラグインの名前
- AssemblyDescription
    - プラグインの説明
- AssemblyVersion
    - プラグインのバージョン

### 1. コードを書く
頑張ってゴリゴリ書きましょう

### 2. 公開する
公開ができる状態になったらmainにpushしてtag打ってreleaseを作りましょう
tagを打つとciが走って自動でreleaseが作られビルド生成物が添付されます


## デバッグについて
※この項目に書いてあることは環境によって差異があるかもしれないので適宜自分の環境に合わせて読み替えること
### 生成物がAtsExから読めるようにする
#### 生成物の出力パスをいじる
1. メニューバー > プロジェクト > (プロジェクト名)のプロパティ を選択しプロジェクトのプロパティ画面を開く
1. サイドバー > ビルド を選択しビルドの設定画面を開く
1. 出力セクションの出力パスをプラグインの出力先に設定する
1. 試しにビルドしてみて出力されるか確認する
#### シンボリックリンクを張る
1. 生成物がない場合はビルドしてダミーのdllを生成する
1. 出力ディレクトリ(binの下)にある生成物へのシンボリックリンクをプラグインの配置場所に配置する
    - winでシンボリックリンクを簡単に張るには[Link Shell Extension](https://www.gigafree.net/system/explorer/hardlinkshellextension.html)がおすすめ
1. 試しにビルドしてみて更新されるか確認する
### Visual Studioでデバッグする
#### デバッグの設定をする
1. メニューバー > デバッグ > (プロジェクト名)のデバッグプロパティ を選択しプロジェクトのデバッグプロパティ画面を開く
1. 開始動作を"外部プログラムの開始"を選択しBveのパスを設定する
1. 必要があればコマンドライン引数にシナリオファイルのパスを設定する
    - ここでシナリオファイルのパスを設定したらそのシナリオが直接読み込まれる
    - 何も指定しなければ普通にシナリオ選択画面が立ち上がる
#### 実際にデバッグする
1. 適当にブレークとかを張る
1. デバッグを始める
    - F5キー
    - メニューバーのデバッグとテストの下あたりの開始ボタン（緑の三角形）
1. 張ったブレークで止まるか見てみる


## 備考・その他
- C#は初めてなのでお作法がわかりません
    - ミスとか良くないところがあったらissue立てるなりしてくれればできる範囲で対応します
    - PR大歓迎！！！
- 自分用に作ったので適当です、自分が欲しい機能をとりあえず入れてます
- AtsExとAtsEXがどっちもあったのでここでは引用を除いてコードに準じてAtsExとしています
    - AtsEXが正式な表記っぽい？
