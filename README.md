□freenoveのESP32CAMでローバーを動かすプロジェクト
・PlatformIOのプロジェクトになっています

〇Camera Web Serverへの要素追加
Camera Web Serverのメニューに
GPIO 12
GPIO 13
GPIO 14
GPIO 15
のDutyコントロールを追加しています
メインメニューのLEDコントロールで
GPIO2のDutyコントロールも入れています


〇ローバーのコントロール
    Forward
LEFT STOP RIGHT
     BACK
の並びでボタンを配置
それぞれのボタンで
GPIOピンを制御することで
ローバーを動かします
