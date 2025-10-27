# 第5回 Webエンジニアリング演習 レポート
## 学籍番号
4723113
## 各エンドポイントのSwagger UIでのテスト結果
### GET /
'''
Request:
curl -X 'GET' \
  'http://localhost:8000/' \
  -H 'accept: application/json'
Response:
{
  "Hello": "World"
}
'''
### GET /health
'''
Request:
curl -X 'GET' \
  'http://localhost:8000/health' \
  -H 'accept: application/json'
Response:
{
  "status": "healthy"
}
'''
### GET /items/{item_id}
'''
Request:
curl -X 'GET' \
  'http://localhost:8000/items/5?q=aaa' \
  -H 'accept: application/json'
Response:
{
  "item_id": 5,
  "q": "aaa"
}
'''
### GET /items/{item_id}エラーハンドリングのテスト
'''
Request:
curl -X 'GET' \
  'http://localhost:8000/items/-3' \
  -H 'accept: application/json'
Response:
{
  "detail": "Item ID must be positive"
}
'''