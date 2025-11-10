# 第7回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723113
## PUTリクエスト検証用のモデルとAPI部分のコード
class TodoItemPUTCreateSchema(BaseModel):
    title: Optional[str] = None
    description: Optional[str] = None
    completed: Optional[bool] = None

@app.put("/todos/{todo_id}", response_model=TodoItem)
def put_todo(todo_id: int, req: TodoItemPUTCreateSchema):
    for i, todo in enumerate(todos):
        if todo.id == todo_id:
            todo.title = req.title if req.title is not None else todo.title
            todo.description = req.description if req.description is not None else todo.description
            todo.completed = req.completed if req.completed is not None else todo.completed
            return todo
    raise HTTPException(status_code=404, detail=f"ID {todo_id} のTODOが見つかりません")
## 動作確認結果
- Swagger UIでのPUTエンドポイントテスト結果
- 正常系：存在するタスクの更新
curl -X 'PUT' \
  'http://127.0.0.1:8000/todos/1' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "title": "string",
  "description": "string",
  "completed": true
}'

	
Response body
{
  "id": 1,
  "title": "string",
  "description": "string",
  "completed": true
}
- 異常系：存在しないタスクIDでのエラー確認
curl -X 'PUT' \
  'http://127.0.0.1:8000/todos/10' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "title": "string",
  "description": "string",
  "completed": true
}'

Response body
{
  "detail": "ID 10 のTODOが見つかりません"
}