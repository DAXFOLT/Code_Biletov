# Code_Biletov
Билет 21 
Вопрос 3
Пример структуры базы данныйх:
```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    password_hash VARCHAR(255),
    role VARCHAR(20) -- 'admin' или 'editor'
);

CREATE TABLE articles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    content TEXT,
    author_id INT,
    status VARCHAR(20) -- 'draft' или 'published'
);
```
