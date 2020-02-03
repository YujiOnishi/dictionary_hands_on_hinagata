# dictionary_hands_on

このリポジトリは2020/1/29に開催されるFlutter Handson Osaka #1に利用します。



[TOC]




## 機能概要

自動翻訳機能付きの単語帳アプリ作成のための雛形です。



## 開発環境に必要なもの一覧

AndroidStudio…プログラムを書くために必要

flutter…今回の主役。モバイルアプリ作成のために必要。

firebase…ミドルウェアに採択。DBと自動翻訳のAPIのために必要。




## 環境構築

※flutterでAndroidのシミュレーターが確認できる方はflutterの項目を飛ばしてください※



### 【flutter】

#### ・windowsの方

1. Flutter SDKのダウンロード
2. flutterを起動する
3. AndroidStudioのインストール
4. OS共通の作業へ



#### 1,Flutter SDKのダウンロード

①以下より任意の場所にダウンロード

https://storage.googleapis.com/flutter_infra/releases/stable/windows/flutter_windows_v1.9.1+hotfix.6-stable.zip

※リンク切れなら[こちら](https://flutter.dev/docs/get-started/install/windows)の指示に従ってSDKをダウンロードしてください。



#### 2,flutterを起動する

※以下の作業をC:\Program Filesのようなアクセス許可が必要な場所で行うと失敗しますので注意してください※

①C直下に[src]フォルダ作成

②1でダウンロードしたC:\src直下に解凍



#### 3,AndroidStudioのインストール

①以下より任意の場所に.exeをダウンロード

https://developer.android.com/studio/?hl=ja

②インストールウィザードの指示に従ってインストール

※初回起動時にSDKのインストールウィザードが出るがStandardを選択肢デフォルトの設定でインストール

※HAXMのインストールでエラーが出る場合以下参照※

①コマンドプロンプトを管理者権限で開く
②以下コマンドを叩いて再起動
bcdedit/set hypervisorlaunchtype off

③BIOSを起動してVT-xを有効化

④configureからsdk managerを起動しSDK ToolsからHAXMにチェックを入れokを押下。

※HAXMにチェックがすでに入っていたら一旦外してApplyする



#### 4,OS共通の作業へ

①下部「macの方」項目を飛ばして「OS共通」項目の作業へ。



#### ・macの方

1. Flutter SDKのダウンロード＆解凍
2. パスを通す
3. AndroidStudioのインストール
4. OS共通の作業へ



#### 1,Flutter SDKのダウンロード＆解凍

①以下より「Downloads」にダウンロード＆解凍

https://storage.googleapis.com/flutter_infra/releases/stable/macos/flutter_macos_v1.9.1+hotfix.6-stable.zip

※リンク切れなら[こちら](https://flutter.dev/docs/get-started/install/windows)の指示に従ってSDKをダウンロードしてください。



②以下コマンドを叩く

```
mkdir ~/development
```
先程のzipを解答してdevelopmentフォルダに移動


#### 2,パスを通す

①bash_profileをviで開く

以下コマンドを叩く

```
vi ~/.bash_profile
```



②以下を追加

```
export PATH="$PATH:/Users/[User名に置き換えて[]を削除]/development/flutter/bin"
```



③pathを更新

以下コマンドを叩く

```
source ~/.bash_profile
```



#### 3.AndroidStudioのインストール

①以下より任意の場所にインストールファイルをダウンロード

https://developer.android.com/studio/?hl=ja

②インストールウィザードの指示に従ってインストール

※初回起動時にSDKのインストールウィザードが出るがStandardを選択肢デフォルトの設定でインストール



#### 4.OS共通の作業へ

①「OS共通」項目の作業へ。



#### ・OS共通

1. flutter doctor --android-licenses
2. Flutterプラグインのインストール
3. エミュレータの作成



#### 1,flutter doctor --android-licenses

①以下コマンドを叩く

※Windowsの方はC:\src\flutterflutter_console.batを起動しそちらで叩く

```
flutter doctor --android-licenses
```



#### 2,Flutterプラグインのインストール

※flutterプラグインのインストールの際、Dartプラグインもインストールするか尋ねられるので合わせてインストールする※

①AndroidStudioを起動する

※初回起動時にSDKのインストールウィザードが出るがStandardを選択肢デフォルトの設定でインストール

②configureを押下。メニュー一覧が表示されるはずなのでPluginを選択する。

③検索ボックスからflutterと検索し、公式のflutter.ioが提供するflutterプラグインを選択しインストールを押してFlutterプラグインとDartプラグインをインストールする。



#### 2,エミュレータの作成

①configureを押下し、AVD Managerを起動
②create virtual deviceを押下
③Pixel2を選択しnextを押下
④システムイメージのAPIレベルを求められるので29(Q)を選択しnextを押下。
※この際、SystemImageが未ダウンロードであればReleaseNameにDownloadと表示されているはずなのでダウンロードする。
⑤finishを押下



### 【firebase】

※前提…グーグルアカウントを取得していること

1. firebaseの登録
2. データベースの作成
3. firebase extentionsの登録
4. アプリ登録

#### 1,firebaseの登録

①以下のURLにアクセスし「使ってみる」を押下
https://firebase.google.com/?hl=ja

②プロジェクトの作成（手順 1/3）「プロジェクトに名前を付けましょう」

「氏名(ローマ字)-dictionary-hands-on」と名前をつけて続行を押下。
※プロジェクト名は任意なのでなんでもいい※



③プロジェクトの作成（手順 2/3）「Google アナリティクス」

Googleアナリティクスを有効にするにチェックを入れ続行を押下。



④プロジェクトの作成（手順 3/3）「Google アナリティクスの構成」

全てチェックしてプロジェクト作成を押下。



#### 2,データベースの作成

①作成したプロジェクトページを開いてサイドメニューの「開発」を押下。

②「Database」を押下。

③「データベースの作成」を押下。

④テストモードで開始にチェックを入れ「次へ」を押下。

⑤Cloud Firestore のロケーション をasia-northeast1にして「完了」を押下。

---------------以下2020/2/3追記---------------

⑥「インデックス」を押下

⑦「インデックスを追加」を押下し

⑧以下の設定を行いインデックスを作成。

コレクションID→dictionary

フィールドのパス1→word,Ascending

フィールドのパス2→created_at,Descending

クエリのスコープ→コレクション

---------------------------------------------


#### 3,firebase extentionsの登録

※お支払い情報を入力する作業がありますが個人で普通に使っている分だと無料枠を超えることはありません※

①作成したプロジェクトページを開いてサイドメニューの「Extentions」を押下。

②Translate Textの「インストール」を押下。

③「次へ」を押下

④「プロジェクトをアップグレード」を押下。

⑤指示に従ってお支払い情報を入力する。


#### 4,アプリ登録

①Project Overviewの「Android」を押下し、Androidを選択。

※次回以降はProject Overview上部の「アプリ追加」を押下し、Androidを選択。

②Androidパッケージ名に「com.example.dictionary」と入力し「登録」を押下。

③google.service.jsonをダウンロードする。



---------------以下2020/2/3追記---------------

#### 5,translate textのインストール
①作成したプロジェクトページを開いてサイドメニューの「extentions」を押下。

②Translate Textを探してインストール。

③translation language for～の設定を「en,ja」に設定。（frやesなどをプラスしても問題ありません）

④collection pathを「dictionary」と設定。

⑤input fieldnameを「word」と設定。

⑥output fieldnameを「translated」と設定。

---------------------------------------------

## サンプルアプリ起動

1. git clone
2. Get dependencies
3. gradle sync
4. エミュレータ起動
5. アプリ起動



#### 1,git clone

①以下リポジトリをクローン
https://github.com/YujiOnishi/dictionary_hands_on_hinagata.git



#### 2, Get dependencies

①AndroidStudioで「dictionary_hands_on_hinagata」フォルダを開く

②「dictionary_hands_on_hinagata/lib/main.dart」を開くと上部にGet dependencyと表示されているはずなので押下。



#### 3,gradle sync

①firebaseの設定項目でダウンロードしたgoogle.service.jsonを「dictionary_hands_on_hinagata/android/app」に移動。

②AndroidStudioで「dictionary_hands_on_hinagata/android」フォルダを開くと自動でgradle syncが始まる





#### 4,エミュレータ起動

①AndroidStudioで「dictionary_hands_on_hinagata」フォルダを開く

②AVDマネージャーから作成したエミュレータを起動する



#### 5,アプリ起動

①上部の再生ボタンを押下しアプリを起動。
※結構時間がかかります※



## 困ったら…

 [公式ドキュメントを読みましょう](http://flutter.io/)http://flutter.io/)
