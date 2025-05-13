```mermaid
erDiagram
    USER ||--o{ PROFILE : has
    USER {
        INTEGER id PK
        VARCHAR username
        VARCHAR password
        VARCHAR email UNIQUE
        DATETIME created_at
        DATETIME updated_at
    }
    PROFILE {
        INTEGER user_id FK
        VARCHAR first_name
        VARCHAR last_name
        DATE birth_date
        TEXT bio
        VARCHAR phone_number
        VARCHAR avatar_url
        DATETIME updated_at
    }
    CATEGORY ||--o{ ARTICLE : has
    ARTICLE {
        INTEGER id PK
        INTEGER category_id FK
        INTEGER author_id FK
        VARCHAR title
        TEXT content
        VARCHAR slug UNIQUE
        DATETIME published_at
        DATETIME created_at
        DATETIME updated_at
    }
    AUTHOR ||--o{ ARTICLE : writes
    AUTHOR {
        INTEGER id PK
        VARCHAR name
        TEXT bio
        VARCHAR email UNIQUE
        DATETIME created_at
        DATETIME updated_at
    }
    TAG ||--o{ ARTICLE_TAG : has
    ARTICLE ||--o{ ARTICLE_TAG : contains
    ARTICLE_TAG {
        INTEGER article_id FK
        INTEGER tag_id FK
        PRIMARY KEY (article_id, tag_id)
    }
    TAG {
        INTEGER id PK
        VARCHAR name UNIQUE
        DATETIME created_at
        DATETIME updated_at
    }
    USER ||--o{ COMMENT : posts
    ARTICLE ||--o{ COMMENT : has
    COMMENT {
        INTEGER id PK
        INTEGER user_id FK
        INTEGER article_id FK
        TEXT content
        DATETIME created_at
        DATETIME updated_at
    }
    USER ||--o{ TOKEN : owns
    TOKEN {
        INTEGER id PK
        INTEGER user_id FK
        VARCHAR token UNIQUE
        DATETIME expiry_at
        DATETIME created_at
    }
