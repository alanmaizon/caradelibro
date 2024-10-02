# caradelibro
ERD for a social media platform
```mermaid
erDiagram
    USER {
        int id PK
        string username
        string email
        string password
        datetime created_at
        string profile_picture
        text bio
    }

    FRIENDSHIP {
        int user_id PK, FK
        int friend_id PK, FK
        datetime created_at
    }

    POST {
        int id PK
        int user_id FK
        text content
        string media_url
        datetime created_at
    }

    COMMENT {
        int id PK
        int post_id FK
        int user_id FK
        text content
        datetime created_at
    }

    LIKE {
        int post_id PK, FK
        int user_id PK, FK
        datetime created_at
    }

    ADMIN {
        int id PK
        string username
        string email
        string password
    }

    MODERATION_ACTION {
        int id PK
        int admin_id FK
        int user_id FK
        string action
        datetime created_at
    }

    USER ||--o{ FRIENDSHIP : "has"
    USER ||--o{ POST : "creates"
    USER ||--o{ COMMENT : "writes"
    USER ||--o{ LIKE : "gives"
    POST ||--o{ COMMENT : "receives"
    POST ||--o{ LIKE : "receives"
    ADMIN ||--o{ MODERATION_ACTION : "performs"
    USER ||--o{ MODERATION_ACTION : "is targeted by"
