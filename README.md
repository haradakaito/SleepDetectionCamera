# [Zoom用] 居眠り検知カメラ
## 0. システム概要
![zoomcamera_system](https://github.com/haradakaito/SleepDetectionCamera/assets/75819611/bdcb242a-b6f4-424d-9cf0-d7f09494bb5d)

## 1. 環境構築
- OpenCVのインストール
```
$ pip install opencv-python
```
> OpenCVとはインテルが開発・公開したオープンソースのコンピュータビジョン向けライブラリ

- OBS Studioのインストール  
[OBS Studio公式ダウンロードページ](https://obsproject.com/ja/download)からインストール可能
> OBS Studio（オービーエススタジオ，OBS，Open Broadcaster Software）は、OBS Projectが開発保守しているフリー・オープンなストリーミング配信・録画ソフトウェア
- Zoomのインストール  
[Zoomデスクトップアプリダウンロードページ](https://zoom.us/download#client_4meeting) から入手可能.  
※ ブラウザ版でもデスクトップアプリ版でもどちらでも良い

## 2. アルゴリズム
- OpenCVで，デバイス搭載のカメラを起動する
- OBS Studioで，OpenCVで起動したカメラウィンドウを仮想カメラとして映す
- Zoomを起動し，ビデオで"OBS Studioの仮想カメラ"を選択することで, OpenCVで起動したカメラウィンドウをZoomに映すことが可能になる
- ZoomカメラのON/OFFの切り替えに関しては, Zoom画面のビデオON/OFF切り替えボタンに割り当てられているキーコマンド(Alt+V)を実行することで実現している  
※Zoomのウィンドウをカーソル選択している時でなければ, ビデオON/OFFはできないことである(他のウィンドウ上で変な挙動をしてしまう恐れがある)

<img width=500 src=https://github.com/haradakaito/SleepDetectionCamera/assets/75819611/30b25d30-e699-4491-871f-5ffcd4ef2bed>

上図に，OpenCVカメラ制御時のフローチャートを示す. 
- OpenCVカメラの映像を入力として，顔(目と口)を認識するための学習済みモデルに与える
- カメラが目を認識している間は，タイマーをリセットし，カメラをONにする操作を繰り返す
- 目が認識されていない時間が一定時間を経過した場合，カメラをOFFにする
