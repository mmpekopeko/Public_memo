##### フロントエンド側の全体構成

```
src
|
+-- assets            # assetsフォルダには、画像やフォントなど、すべての静的ファイルを格納できます
|
+-- components        # アプリケーション全体で使用される共有コンポーネント
|
+-- constants         # アプリケーション全体で使用される定数を管理
|
+-- features          # 機能ベースモジュール
|
+-- hooks             # アプリケーション全体で使用される共有フック
|
+-- lib               # アプリケーション用にあらかじめ設定された異なるライブラリの再エクスポート
|
+-- mocks             # APIモックサーバーを管理
|
+-- providers         # すべてのアプリケーションプロバイダ
|
+-- routes            # ルート構成
|
+-- state             # グローバルステータスStore
|
+-- types             # アプリケーションで使用される基本の型定義
|
+-- utils             # 共通関数等

```

##### src/page/hogehoge

```
|
+-- api            # 特定の画面に関連するエクスポートされたAPIリクエスト宣言とapiフック
|                 useで始まるファイルではないが、exportしているのはuse～なので正真正銘フックなので問題なし
+-- components     # 特定の画面にスコープされたコンポーネント
|
+-- constants      # 特定の画面で使用される定数を管理
|
+-- hooks          # 特定の画面にスコープされたhooks
|
+-- routes         # 特定の画面ページのためのルートコンポーネント
|      |
|      +-- Hogehoge.tsx
|
+-- types          # 特定画面用の型定義
|
+-- utils          # 特定画面用の関数など
|
+-- index.ts       # その画面のエントリポイントであり、与えられた画面のパブリックAPIとして画面し、その画面の外部で使用されるべきすべてのものをエクスポートします。
|
+-- validations.ts # 特定の画面用のバリデーション定義ファイル

```

##### 共通コンポーネントの構成

```

src
|
+-- components     # アプリケーション全体で使用される共有コンポーネント
  |
  +-- Elements     # ButtonやDialog等の要素
  |
  +-- Form         # フォームで使用する入力項目
  |
  +-- Head         # HTMLのHEAD情報管理
  |
  +-- Layout       # 画面レイアウト

```

master_0_202311241525.zip
master_1_2023XXXXXXXX.zip
master_2_2023XXXXXXXX.zip  
master_3_2023XXXXXXXX.zip



ソース履歴

```
履歴番号　マージしたソース	元のソース	         コメント				備考		担当　　日付
1	  master_1_2023XXXXXXXX.zip    master_0_202311241525.zip 　01 ログイン画面 ○○の修正　　	田中　　	2023/11/27	
												ID: user
												パスワード：user
												ログインは可能
												ログイン後の画面遷移は未実装

2 	 master_2_2023XXXXXXXX.zip       master_1_2023XXXXXXXX.zip   09 ○○画面の新規追加	山田		2023/11/28
3	 master_3_2023XXXXXXXX.zip　　master_2_2023XXXXXXXX.zip   	09 ○○画面の機能修正　　　　　　　　　　　　　山田　　2023/12/01
4
```
