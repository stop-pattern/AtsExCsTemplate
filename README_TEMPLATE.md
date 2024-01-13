# READMEのテンプレート
## 使い方
1. 既にある`README.md`を消す
2. このテンプレートを`README.md`にリネームする
3. 水平線より上(この使い方の部分)を消す
4. `$REPONAME$`をリポジトリの名前に置換する
5. Todoのところを書く
6. 保存してコミット&プッシュ
---
# $REPONAME$
[AtsEX](https://github.com/automatic9045/AtsEX)を使ったBve5またはBve6用のプラグイン
**Todo: プラグインの概要を書く**


## プラグインの機能
- **Todo: 機能を列挙**


## 導入方法
**Todo: 導入方法を必要に応じて変更**
### 1. AtsEXの導入
[公式のダウンロードページ](https://automatic9045.github.io/AtsEX/download/)を参照してください
### 2. 本プラグインの導入
1. [Releases](releases/)から最新版がダウンロードできます
2. **Todo: 配置場所をプラグインの種類に応じて下から選択して変更**
```md
# 拡張機能の場合
2. AtsExの導入場所にある`Extensions`フォルダの中に本プラグインを配置します
    - デフォルト: `C:\Users\Public\Documents\AtsEx\1.0\Extensions`
    - プラグインはBveの起動と同時に読み込まれ、必要に応じて他のプラグインから利用されます

# マッププラグインの場合
2. シナリオフォルダの中に本プラグインを配置します  
    ディレクトリ構成例: 
    ```text
    Scenarios
    ├ MyScenario.txt
    └ MyMaps
      └ SampleMap
        ├ MapPlugins
        │ ├ 本プラグイン($REPONAME$.dll)
        │ ├ OtherPlugin.dll
        │ └ ...
        ├ MapPluginUsing.xml
        ├ Image.jpg
        ├ Map.txt
        ├ Signals.csv
        ├ Sounds.csv
        ├ Sounds3D.csv
        ├ Stations.csv
        └ Structures.csv
    ```
3. `MapPluginUsing.xml`を作成し本プラグインの情報を記入します  
    MapPluginUsing.xml(例): 
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <AtsExPluginUsing xmlns="http://automatic9045.github.io/ns/xmlschemas/AtsExPluginUsingXmlSchema.xsd">
    	<Assembly Path="MapPlugins\$REPONAME$.dll" />
    	<Assembly Path="MapPlugins\OtherPlugin.dll" />
    </AtsExPluginUsing>
    ```
4. マップファイルから参照します  
    Map.txt(例): 
    ```text
    BveTs Map 2.02:utf-8
    
    // AtsEX
    include '<AtsEx::USEATSEX>';                            // AtsEXのプラグインを使うという宣言
    include '<AtsEx::READDEPTH>1';                          // AtsEXのプラグインを探すディレクトリの深さ
    include '<AtsEx::MapPluginUsing>MapPluginUsing.xml';    // 使うプラグインの情報を伝えるファイルの位置
    
    Structure.Load('Structures.txt');
    Signal.Load('Signals.csv');
    Sound.Load('Sounds_e.txt');
    Sound3D.Load('Sounds3D.txt');
    Station.Load('Stations.csv');
    
    0;
    ...
    ```

# 車両プラグインの場合
2. 車両アドオンの中に本プラグインを配置します  
    ディレクトリ構成例: 
    ```text
    Scenarios
    └ MyVehicles
    　 └ SampleVehicle
    　 　 ├ Vehicle.txt
    　 　 ├ Ats
    　 　 │ ├ AtsEx.Caller.txt
    　 　 │ ├ AtsEx.Caller.x64.dll
    　 　 │ ├ AtsEx.Caller.x86.dll
    　 　 │ ├ AtsEXPlugins
    　 　 │ │ ├ 本プラグイン($REPONAME$.dll)
    　 　 │ │ └ OtherPlugin.dll
    　 　 │ ├ DetailManager.x64.dll
    　 　 │ ├ DetailManager.x86.dll
    　 　 │ ├ detailmodules.txt
    　 　 │ ├ OtherNormalPlugin.dll
    　 　 │ └ ...
    　 　 ├ Notch
    　 　 │ ├ Notch.txt
    　 　 │ └ ...
    　 　 ├ Panel
    　 　 │ ├ Panel.txt
    　 　 │ └ ...
    　 　 ├ Sound
    　 　 │ ├ Sound.txt
    　 　 │ ├ Motor.txt
    　 　 │ └ ...
    　 　 ├ Parameters.txt
    　 　 └ ...
    ```
3. 設定ファイルを作成し本プラグインの情報を記入します  
    - AtsEx.Caller.txt
        ```text
        ..\..\..\AtsEx
        ```
    - AtsEx.Caller.x86.VehiclePluginUsing.xml: x64と同じ
    - AtsEx.Caller.x64.VehiclePluginUsing.xml(例): 
        ```xml
        <?xml version="1.0" encoding="utf-8" ?>
        <AtsExPluginUsing xmlns="http://automatic9045.github.io/ns/xmlschemas/AtsExPluginUsingXmlSchema.xsd">
        	<Assembly Path="AtsEXPlugins\$REPONAME$.dll" />
        	<Assembly Path="AtsEXPlugins\OtherPlugin.dll" />
        </AtsExPluginUsing>
        ```
    - AtsEx.Caller.x86.VehicleConfig.xml: x64と同じ
    - AtsEx.Caller.x64.VehicleConfig.xml(例): 
        ```xml
        <?xml version="1.0" encoding="utf-8" ?>
        <AtsExVehicleConfig xmlns="http://automatic9045.github.io/ns/xmlschemas/AtsExVehicleConfigXmlSchema.xsd">
            <DetectSoundIndexConflict>true</DetectSoundIndexConflict>
            <DetectPanelValueIndexConflict>true</DetectPanelValueIndexConflict>
        </AtsExVehicleConfig>
        ```
4. ビークルファイルから参照します  
    Vehicle.txt(例): 
    ```text
    BveTs Vehicle 2.00
    PerformanceCurve = Notch\Notch.txt
    Parameters = Parameters.txt
    Panel = Panel\Panel.txt
    Sound = Sound\Sound.txt
    MotorNoise = Sound\Motor.txt
    Ats32 = Ats\AtsEx.Caller.x86.dll
    Ats64 = Ats\AtsEx.Caller.x64.dll
    ```

   非AtsEXなプラグインと両立する場合は次の通りです
   1. Ats32とAts64でDetailManagerを指定する
   2. detailmodules.txtでAtsEx.Callerを指定する
```
> [!WARNING]
> この項目の内容はすべてが正しい保証がありません
> 正確な情報を得るには以下を参照してください
> - AtsEXの[公式リポジトリ](https://github.com/automatic9045/AtsEX/)
> - AtsEXの[公式サイト](https://automatic9045.github.io/AtsEX/)


## 使い方
- **Todo: 必要に応じて書く**
### パネル
**Todo: 必要に応じて書く**
| index  | 型   | 機能       | 備考              |
| ------ | ---- | ---------- | ----------------- |
| ats001 | uint | 速度絶対値 | 1km刻みで切り捨て |


## ライセンス
- **Todo: `LICENSE`の著作権表示を書き換える**
- **Todo: ライセンスを変更する場合には`LICENSE`を書き換えた後にここも変更する**
- [MIT](LICENSE)
    - できること
        - 商用利用
        - 修正
        - 配布
        - 私的使用
    - ダメなこと
        - 著作者は一切責任を負わない
        - 本プラグインは無保証で提供される


## 動作環境
**Todo: 動作環境を必要に応じて変更**
- Windows
    - Win10 22H2
    - Win11 23H2 or later
- [Bve](https://bvets.net/)
    - BVE Trainsim Version 5.8.7554.391 or later
    - BVE Trainsim Version 6.0.7554.619 or later
- [AtsEX](https://github.com/automatic9045/AtsEX)
    - [ver1.0-RC5 - v1.0.40101.1](https://github.com/automatic9045/AtsEX/releases/tag/v1.0.40101.1) or later


## 開発環境
**Todo: 開発環境を必要に応じて変更**
- [AtsEX](https://github.com/automatic9045/AtsEX)
    - [ver1.0-RC5 - v1.0.40101.1](https://github.com/automatic9045/AtsEX/releases/tag/v1.0.40101.1)
- Win10 22H2
    - Visual Studio 2022
        - Microsoft Visual Studio Community 2022 (64 ビット) - Current Version 17.5.3
- [Bve](https://bvets.net/)
    - BVE Trainsim Version 5.8.7554.391
    - BVE Trainsim Version 6.0.7554.619


## 依存環境
**Todo: 依存環境を必要に応じて変更**
- AtsEx.CoreExtensions (1.0.0-rc1)
- AtsEx.PluginHost (1.0.0-rc5)

(開発者向け)  
間接参照を含めたすべての依存情報については、各プロジェクトのフォルダにある `packages.lock.json` をご確認ください。
