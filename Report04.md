# 第4回 Webエンジニアリング演習 レポート
## 4723113

## 実装したプログラム
- `book_manager.py`の内容と処理の説明
import sys
import json

books = [
    {
        "title": "Java基礎",
        "author": "佐藤花子",
        "year": 2023,
        "isbn": "978-4-987654-32-1",
        "price": 2800
    },
    {
        "title": "Web開発",
        "author": "山田次郎",
        "year": 2023,
        "isbn": "978-4-111111-11-1",
        "price": 3200
    }
]


new_data_json = sys.argv[1]
new_data = json.loads(new_data_json)
books.append(new_data)

for i, book in enumerate(books, start=1):
    print(f"{i}. {book["title"]} - {book["author"]} ({book["year"]}) ISBN: {book["isbn"]} 価格: {book["price"]}円")

## 実行結果    
@4723113 ➜ /workspaces/WE-Python (main) $ python book_manager.py "{ \"title\": \"Python入門\", \"author\": \"田中太郎\", \"year\": 2024, \"isbn\": \"978-4-123456-78-9\", \"price\": 2500 }"
1. Java基礎 - 佐藤花子 (2023) ISBN: 978-4-987654-32-1 価格: 2800円
2. Web開発 - 山田次郎 (2023) ISBN: 978-4-111111-11-1 価格: 3200円
3. Python入門 - 田中太郎 (2024) ISBN: 978-4-123456-78-9 価格: 2500円