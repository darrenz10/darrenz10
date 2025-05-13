```mermaid
erDiagram
    USER ||--o{ PROFILE : has
    USER {
        INTEGER id PK
        VARCHAR username
        VARCHAR email UNIQUE
        VARCHAR password
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
    USER ||--o{ TOKEN : has
    TOKEN {
        INTEGER user_id FK
        VARCHAR token UNIQUE
        DATETIME expiry_at
        DATETIME created_at
    }
    KATEGORI ||--o{ BERITA : contains
    KATEGORI {
        INTEGER id PK
        VARCHAR nama_kategori UNIQUE
        TEXT deskripsi
        DATETIME created_at
        DATETIME updated_at
    }
    BERITA {
        INTEGER id PK
        INTEGER kategori_id FK
        INTEGER penulis_id FK
        VARCHAR judul
        TEXT slug UNIQUE
        TEXT konten
        VARCHAR gambar_utama
        DATETIME tanggal_publikasi
        BOOLEAN is_published
        INTEGER jumlah_dibaca
        DATETIME created_at
        DATETIME updated_at
    }
    PENULIS ||--o{ BERITA : writes
    PENULIS {
        INTEGER id PK
        VARCHAR nama_lengkap
        VARCHAR email UNIQUE
        TEXT bio
        DATETIME created_at
        DATETIME updated_at
    }
    BERITA ||--o{ TAG : has
    TAG {
        INTEGER id PK
        VARCHAR nama_tag UNIQUE
        DATETIME created_at
        DATETIME updated_at
    }
    BERITA_TAGS {
        INTEGER berita_id FK
        INTEGER tag_id FK
        PRIMARY KEY (berita_id, tag_id)
    }
    BERITA_TAGS }o--|| BERITA : is_related_to
    BERITA_TAGS }o--|| TAG : has
