## 1 バリデーション
### 1.1 バリデーションの実装場所
モデル
### 1.2 バリデーション評価のタイミング
#### バリデーション評価を呼び出すメソッド
モデルのDBテーブルに対して更新するメソッドを呼び出したとき
#### 任意のタイミングで
valid? invalid?
```ruby
if @book.valid?
# 正常な処理
else 
# エラー処理
end
```
バリデーションの評価結果に対するエラー情報は、バリデーション評価メソッドを実行したレシーバー（対象インスタンス）に組み込まれ。そのインスタンスに対してerrorsメソッドで確認できます。

### 1.3 バリデーションの実装方法
- 標準のバリデーションメソッドによる`validates`メソッド
- 独自メソッドを`validate`メソッドで
- 独自Validatorクラスを使用して

### 1.4 標準バリデーションヘルパー
### 1.5 標準バリデーションヘルパー使用例
### 1.6 バリデーションオプション
message
### 1.7 フォームオブジェクトの簡単な実装例（利用許諾）
### エラーメッセージの操作法
```console
app/models/user.rb:20:in `follow'
app/controllers/follow_relations_controller.rb:6:in `create'
Started POST "/follow_relations" for 127.0.0.1 at 2022-05-13 22:21:49 +0900
Processing by FollowRelationsController#create as HTML
  Parameters: {"authenticity_token"=>"[FILTERED]", "followed_id"=>"1", "commit"=>"フォローする"}
   (0.1ms)  SELECT sqlite_version(*)
  User Load (0.2ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? ORDER BY "users"."id" ASC LIMIT ?  [["id", 51], ["LIMIT", 1]]
  User Load (0.6ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
  ↳ app/controllers/follow_relations_controller.rb:5:in `create'
  TRANSACTION (0.1ms)  begin transaction
  ↳ app/models/user.rb:20:in `follow'
  FollowRelation Exists? (0.1ms)  SELECT 1 AS one FROM "follow_relations" WHERE "follow_relations"."follower_id" = ? AND "follow_relations"."followed_id" = ? LIMIT ?  [["follower_id", 51], ["followed_id", 1], ["LIMIT", 1]]
  ↳ app/models/user.rb:20:in `follow'
  TRANSACTION (0.1ms)  rollback transaction
  ↳ app/models/user.rb:20:in `follow'
Completed 422 Unprocessable Entity in 50ms (ActiveRecord: 2.8ms | Allocations: 18967)


  
ActiveRecord::RecordInvalid (バリデーションに失敗しました: Followerはすでに存在します):
  
app/models/user.rb:20:in `follow'
app/controllers/follow_relations_controller.rb:6:in `create'
```



