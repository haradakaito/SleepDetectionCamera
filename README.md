# [Zoom会議用] 居眠り検知カメラ
## 環境構築
- OpenCVのインストール
```
$ pip install opencv-python
```
- OBS Studioのインストール
> OBS Studio（オービーエススタジオ、OBS、Open Broadcaster Software）は、OBS Projectが開発保守しているフリー・オープンなストリーミング配信・録画ソフトウェア

[OBS Studio公式ダウンロードページ](https://obsproject.com/ja/download)からインストール可能
- Zoomのインストール  
[Zoomデスクトップアプリダウンロードページ](https://zoom.us/download#client_4meeting) から入手可能.  
※ ブラウザ版でもデスクトップアプリ版でもどちらでも良い

## システム概要

<img width=500 src=https://github.com/haradakaito/SleepDetectionCamera/assets/75819611/f272725f-5fdc-4019-a2f8-2944e5cc0ed8>

## 実現方法
　OpenCVを用いて, PCカメラを起動し, OBS Studioの仮想カメラでその映像を映している状態でZoomカメラでOBS Studioの仮想カメラを選択することで, OpenCVで起動したカメラウィンドウをZoomに映すことが可能になる.  
　ZoomカメラのON/OFFの切り替えに関しては, 実際にOpenCVのカメラを切るとOBS Studioとの接続も切断されてしまうため, Zoom画面のビデオON/OFF切り替えボタンに割り当てられているキーコマンド(Alt+V)を実行することで実現している.  
　注意点としては, Zoomのウィンドウをカーソル選択している時でなければ, 当然キーコマンドを打ってもビデオON/OFFはできないことである(他のウィンドウ上で変な挙動をしてしまう恐れがある).  
以下にOpenCVカメラ制御時のフローチャートを示す.  

<img width=500 src=https://github.com/haradakaito/SleepDetectionCamera/assets/75819611/30b25d30-e699-4491-871f-5ffcd4ef2bed>


