# 第8回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723113
## 実装した内容
@app.put("/todos/{todo_id}", response_model=TodoItem_Pydantic) 
async def put_todo(todo_id: int, req: TodoItemUpdate_Pydantic):
    todo = await TodoItem.get(id=todo_id)
    if not todo:
        raise HTTPException(status_code=404, detail=f"ID {todo_id} のTODOが見つかりません")
    
    todo.title = req.title if req.title is not None else todo.title
    todo.description = req.description if req.description is not None else todo.description
    todo.completed = req.completed if req.completed is not None else todo.completed
    await todo.save()
    return todo
## 動作確認結果
（PUTエンドポイントの動作確認結果を記載）
・PUTエンドポイントが正常に動作している
Responses
Curl

curl -X 'PUT' \
  'http://127.0.0.1:8000/todos/1' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "title": "string",
  "description": "string",
  "completed": false
}'
	
Response body
{
  "id": 1,
  "title": "string",
  "description": "string",
  "completed": false
}

・存在しないIDを指定した場合に404エラーが返される
Curl

curl -X 'PUT' \
  'http://127.0.0.1:8000/todos/10' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "title": "string",
  "description": "string",
  "completed": false
}'

Response body

{
  "detail": "Object \"TodoItem\" does not exist"
}

・更新後のTODOアイテムが正しくレスポンスに含まれている
Curl

curl -X 'GET' \
  'http://127.0.0.1:8000/todos' \
  -H 'accept: application/json'
  	
Response body

[
  {
    "id": 1,
    "title": "string",
    "description": "string",
    "completed": false
  },
  {
    "id": 3,
    "title": "string",
    "description": "string",
    "completed": false
  },
  {
    "id": 4,
    "title": "string",
    "description": "string",
    "completed": false
  }
]