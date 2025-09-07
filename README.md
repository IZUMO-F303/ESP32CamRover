# ESP32-CAM MJPEG Streamer with GPIO/LED Control

## 1. 概要

このプロジェクトは、Freenove ESP32-WROVER-CAMボードを使用し、Wi-Fi経由でカメラの映像をMJPEG形式でストリーミング配信するプログラムです。
WebブラウザからアクセスできるUIを提供し、カメラの各種設定や、ボードに接続されたGPIO（12, 13, 14, 15）、および内蔵LEDの制御が可能です。

## 2. 主な機能

-   **MJPEGビデオストリーミング**: Wi-Fiネットワーク内のPCやスマートフォンのWebブラウザで、低遅延の映像ストリーミングを閲覧できます。
-   **Web UIによるカメラ制御**: 解像度、画質、明るさ、コントラストなど、カメラの様々なパラメータをリアルタイムで調整できます。
-   **GPIO制御**: GPIO 12, 13, 14, 15 に接続したデバイス（LEDなど）のON/OFFおよびPWMデューティ比（明るさ）をWeb UIのスライダーで制御できます。
-   **内蔵LED制御**: カメラボード上のフラッシュ用LEDのON/OFFおよび輝度をWeb UIから制御できます。

## 3. ハードウェア要件

-   Freenove ESP32-WROVER-CAM

## 4. セットアップと使用方法

### 4.1. ビルドと書き込み

1.  **Wi-Fi設定**: `src/main.cpp` ファイル内の以下の行を、ご自身のWi-FiアクセスポイントのSSIDとパスワードに書き換えます。
    ```cpp
    const char* ssid = "YOUR_WIFI_SSID";
    const char* password = "YOUR_WIFI_PASSWORD";
    ```
2.  **ビルドと書き込み**: PlatformIO環境で、以下のコマンドを実行してプログラムをESP32ボードに書き込みます。
    ```sh
    pio run -t upload
    ```
3.  **IPアドレスの確認**: 書き込み後、シリアルモニターを起動（ボーレート: 115200）すると、ESP32がWi-Fiに接続し、IPアドレスが表示されます。
    ```
    WiFi connected
    Camera Ready! Use 'http://192.168.x.x' to connect
    ```

### 4.2. 操作方法

-   シリアルモニターに表示されたIPアドレス（例: `http://192.168.x.x`）に、PCやスマートフォンのWebブラウザでアクセスします。
-   表示されたWebページ上で、映像のストリーミング、カメラ設定の変更、GPIOやLEDの制御が行えます。

## 5. 開発者向け情報

### 5.1. Web UIの更新手順

Web UI（操作画面）のレイアウトや機能は `index_ov2640.html` ファイルで定義されています。

1.  プロジェクトのルートディレクトリにある `index_ov2640.html` を直接編集します。
2.  編集後、以下のPythonスクリプトを実行して、HTMLファイルをGzip圧縮し、C++ヘッダーファイル (`camera_index.h`) に変換します。
    ```sh
    python python/encode_html.py
    ```
3.  `camera_index.h` が更新されたら、再度PlatformIOでビルドと書き込みを行ってください。

### 5.2. 補助ツール

-   `python/decode_html.py`: `camera_index.h` から `index_ov2640.html` を復元するためのスクリプトです。
-   `python/displayCAM.py`: Webサーバーを介さず、シリアルポート経由で直接カメラ画像を表示するためのデバッグ用ツールです。（使用するには `SERIAL_PORT` の設定が必要です）
