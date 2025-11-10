# 第6回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723113
## 動作確認
- Swagger UIでのテスト結果を記載
▼ 正常系 (有効であるべき入力)
1. GET /todos/ ではすべてのTODOアイテムが取得できる
[
  {
    "id": 1,
    "title": "牛乳とパンを買う",
    "description": "牛乳は低温殺菌じゃないとだめ",
    "completed": false
  },
  {
    "id": 2,
    "title": "Pythonの勉強",
    "description": "30分勉強する",
    "completed": true
  },
  {
    "id": 3,
    "title": "30分のジョギング",
    "description": "",
    "completed": false
  },
  {
    "id": 4,
    "title": "技術書を読む",
    "description": "",
    "completed": false
  },
  {
    "id": 5,
    "title": "夕食の準備",
    "description": "カレーを作る",
    "completed": true
  }
]
2. GET /todos/?query=牛乳 では、クエリに部分一致したアイテムのリストが取得できる
[
  {
    "id": 1,
    "title": "牛乳とパンを買う",
    "description": "牛乳は低温殺菌じゃないとだめ",
    "completed": false
  }
]
3. GET /todos/?query=存在しない文字列 では０件のリストが取得できる
[]
▼ 異常系 (有効でない入力)
1. 今回は特にないが、通常はエラーメッセージを出すべき入力のテストもする
todo_id 10

Responses:
{
  "detail": "TODOが見つからない"
}