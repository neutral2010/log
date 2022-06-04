## 1.ルーティングとは
ルーター:ブラウザから要求を最初に受け取る窓口
ルート:URIで指定される宛先とHTTPメソッドの組み合わせによってどのコントローラーのどのアクションをよぶ出すのかという振り分けの設定
ルーティング:ルーターがルートに沿って振り分ける作業のこと

### 1.1 HTTPメソッド
### 1.2 ルートの対応関係と実装例
例`GET /users users/index →Userコントローラーのindexアクション
### 1.3 リソースフルルート
7つの標準的アクションについて一括して瀬亭してくれる。
7つの標準的アクションとは、`new,create,edit,update,destroy,show,index`

`resources :user`

![image.png](https://bootcamp.fjord.jp/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBBeFNsQWc9PSIsImV4cCI6bnVsbCwicHVyIjoiYmxvYl9pZCJ9fQ==--ba0b6dee1029cc0e5e84e4185e685c08cf937ffb/image.png)
[Railsを支える基本概念の整理（RESTfulやリソースなど） - Qiita](https://qiita.com/kidach1/items/43e53811c12351915278)

###1.4 非リソースフルルート

## 2. ルート設定とルーティングヘルパー
### 2.1 ルート設定ファイルとルートの確認方法
`routes.rb`

- `rails routes`
- `http://localhost:3000/rails/info/routes`

 ### 2.2 rootの設定方法
 ` root to: 'コントローラー名#アクション名'`
 #### rootメソッドを使用したリダイレクト設定方法
 `root to: redirect('users/index')

 ### 2.3 非リソートフルルートの設定方法

 ### 2.5(4は？) ルーティング（Path／URL）ヘルパー
左端、ルートを設定すると自動でできる。
宛先URLを一語で表現できる。
 ![image.png](https://bootcamp.fjord.jp/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBBeFdsQWc9PSIsImV4cCI6bnVsbCwicHVyIjoiYmxvYl9pZCJ9fQ==--6572b93797e878146b6a7f63cc237cd7d5b34d7f/image.png)
 コントローラーやビューなどRailsアプリケーションの中で、遷移先を簡潔に分かりやすくすることができる。

 ## 3. リソートフルルートをより有効に使う方法
 ### 3.1 リソートフルルートのオプション
 - as
 - only
 - except
 ### 3.2 独自アクションルートを追加する方法
 #### ブロックを使用して追加

 ### 3.3 親子関係を持つ入れ子ルートについて
 親子関係を持つモデル。子のモデルリソースには親を通してしかアクスできない場合。ルートも入れ子に。shallowルート

 ### 3.4リソートフルルートのグループ化
 #### 名前空間を使う
 #### scopeメソッドを使う

 ### 3.5 ルートの共通化 concern, concerns

 ### 3.6 リソートフルルートをしようしたびゅーのURL宛先指定

## 4. コントローラーの役割
ルーターから振り分けられた（送られてきた）要求をもとに、アクション内の処理（インスタンスメソッドで実装されている。）を実行する。

 ### 4.1 コントローラーとREST
 RESTとは「HTTPプロトコルと通じて同じ宛先URIとパラメーターの組み合わせによってリクエストし、常に同じレスポンス結果が得られることを期待する」通信アクセスの仕組みです。
 RailsはRESTを満たしている仕組みで（Restful)、その中心をなす司令塔がコントローラー
 
 ### 4.2 コントローラーの仕組み
 ルーターによって呼び出されたコントローラーがインスタンスかされ、そのインスタンスメソッドが実行されている。

 - HTTPレスポンスの送信時には、ビューを出力するためのレンダリング処理をするか、次の宛先へリダイレクト（再接続要求）する処理を行います。
 - 通常はビューへのレンダリングで終わるので、アクションの最後には、どのビューのレンダリング処理（renderメソッドの実行）をするかが、指定されている必要があるのです。
- インスタンス変数の情報を通す。
- 基本的なRailsアプリケーションの流れ : 「1つのHTTPリクエストに対して該当する１つのアクションが実行されてHTTPレスポンスが送信される」だけ（だが、とても重要）
- アクションはトランサクション機能の役割を果たす。

 ### 3.3 HTTPヘッダー情報などの取得方法
 コントローラーはHTTP通信の情報を参照・取得できる。
 #### HTTPリクエストヘッダーの取得 `request`メソッド
 リクエストオブジェクト

 #### ネットワーク上で使われるのはGETとPOSTだけ
 ルーターの指定がPATCHやDELETEであってもHTTPメソッドはGETとPOSTだけなのが確認できる。（ネットワーク上ではGETとPOSTだけが使われている。）

#### HTTPレスポンスがヘッダーの取得 `response`メソッド
レスポンスオブジェクト
 
