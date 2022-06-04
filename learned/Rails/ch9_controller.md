## 1.1 コントローラーによるデータの扱い
### データ入力と出力の扱い
- コントローラーは要求されたルートで繋がれたアクションの中でクライアントから送信された入力データを受け取る。
- アクションはこの入力データをもとに、モデルをやり取りを通してDBテーブルなどに保存を行う。
- 結果をHTTPレスポンスとしてクライアントへ返す。

別の言い方をすると、、、
- 入力データはコントローラーのアクションにハッシュ型のパラメーター（paramsインスタンス）として渡され利用される。
- 処理した結果はrenderメソッドによって呼び出されたビューテンプレートに埋め込まれ、HTMLに変換されて表示される。

### 1.2 コントローラーが扱うパラメーターと1.3 パラメーターの参照：取得
コンソールログで確認できる
- フォームパラメーター（POSTパラメーター）
画面の入力フォーム（form＿withヘルパーを通して生成されるformタグ）から送信されるデータ。（入力データ）HTTPのPOSTリクエストのメッセージボディを通して渡される。取得方法は`params[:book]``params[:book][:title]`
- ルートパラメーター（パスパラメーター）
リソースを特定する[:id]パラメーターなどが該当する。取得方法は`params[:id]`
- クエリパラメーター

paramsインスタンスにたいして、存在しないキーを指定した場合はnilが発生する。

【注意】
パラメーターは外部から情報を取り込む目的があるため、セキュリティ面で注意すべきポイント
- Railsルールに則ったバリデーション
- DBとの整合性を持つパラメーターを使用する

### 1.4 ストロングパラメーターの役割
マスアサインメントという脆弱性を回避するための手段。許可処理を経由しないパラメーターを無効にする仕組み
```ruby
#books_contololler.rb
private

def book_params
    params.require(:book).permit(:title, :memo, :author, :picture)
end
```

### 1.5 render（表示出力）メソッド
レンダリングはコントローラーのアクションがrenderメソッドを使用してビューの出力を指示する作業。それをもとにアクション内で指示されたインスタンス変数の値などを使ってHTMLを生成します。コントローラーが結果をHTTPレスポンスのデータとしてクライアントへ転送することで、ブラウザ上に表示される。

アクション名と同じ名前のビューで表示する場合は、renderメソッドで明示しなくてもよい。（Railsの規約のうち）

#### 任意のビューテンプレートをレンダリングしたい場合
renderの引数として、ビューの名前を指示。
もし他のコントローラーに関するビューを呼び出す場合は、そのコントローラー名を持つディレクトリから、viewsを起点にした相対パスで指示する。

#### renderメソッドのオプション
#### ビューテンプレートを使用しないレンダリング
#### その他のオプション

### 1.6 redirect_to（宛先変更）メソッド
アクション終了後に他のアクションを実行したい場合、他のサイトに接続したい場合にこのメソッドを使って、HTTPレスポンスを送信する。

#### redirect_toメソッドのオプション
- notice:
- alert:
- flash:

使用例
```ruby
redirect_to @book, notice: 'Book was successfully created'
```
#### url_forメソッド

### 1.7 セッション情報の制御とクッキーの利用

## 2 目的に合わせた出力フォーマットの制御
### 2.1 出力形式の制御
### 2.2 respond_toメソッドの役割

## 3 フィルター
### 3.1 フィルターとは 3.2 before_action実装例
全てのアクションに対して、前処理後処理を設定する役割を提供する。
一回だけ実行される。複数のアクションに共通な処理。
cf コールバック（モデル）

- before_action
- after_action
- around_action

特定のアクションに対するオプション
- except
- only

### 3.3 around_actionによる実装例
yield
### 3.4 フィルターのスキップ機能
### 3.5 HTTP認証とフィルターの活用

(「独習Ruby on Rails」翔泳社　9章）