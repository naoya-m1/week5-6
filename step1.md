# データベースのテーブル定義

## channel_table (チャンネルテーブル)

| フィールド    | データ型     | Null許可 | 主キー | その他          |
|--------------|-------------|----------|-------|----------------|
| channel_id   | BIGINT(20)  | NO       | YES   | AUTO_INCREMENT |
| channel_name | VARCHAR(255)| NO       | UNIQUE|                |

## program_table (番組テーブル)

| フィールド         | データ型    | Null許可 | 主キー | その他          |
|---------------------|-------------|----------|-------|----------------|
| program_id          | BIGINT(20)  | NO       | YES   | AUTO_INCREMENT |
| program_title       | VARCHAR(255)| NO       | UNIQUE|                |
| program_description | TEXT        | YES      |       |                |

## season_table (シーズンテーブル)

| フィールド     | データ型    | Null許可 | 主キー | その他          |
|--------------|------------|----------|-------|----------------|
| season_id    | BIGINT(20) | NO       | YES   | AUTO_INCREMENT |
| season_number| BIGINT(20) | YES      |       |                |
| program_id   | BIGINT(20) | YES      | 外部キー |                |

## episode_table (エピソードテーブル)

| フィールド         | データ型    | Null許可 | 主キー | その他          |
|--------------------|-------------|----------|-------|----------------|
| episode_id         | BIGINT(20)  | NO       | YES   | AUTO_INCREMENT |
| episode_number     | BIGINT(20)  | YES      |       |                |
| episode_title      | VARCHAR(255)| YES      |       |                |
| episode_description| TEXT        | YES      |       |                |
| video_length       | TIME        | YES      |       |                |
| release_date       | DATE        | YES      |       |                |
| views              | BIGINT(20)  | YES      |       | DEFAULT 0      |
| season_id          | BIGINT(20)  | YES      | 外部キー |                |
| program_id         | BIGINT(20)  | YES      | 外部キー |                |

## time_slot_table (時間スロットテーブル)

| フィールド    | データ型    | Null許可 | 主キー | その他          |
|-------------|-------------|----------|-------|----------------|
| time_slot_id| BIGINT(20)  | NO       | YES   | AUTO_INCREMENT |
| start_time  | DATETIME    | YES      |       |                |
| end_time    | DATETIME    | YES      |       |                |
| channel_id  | BIGINT(20)  | YES      | 外部キー |                |
| episode_id  | BIGINT(20)  | YES      | 外部キー |                |

## genre_table (ジャンルテーブル)

| フィールド  | データ型     | Null許可 | 主キー | その他          |
|-----------|-------------|----------|-------|----------------|
| genre_id  | BIGINT(20)  | NO       | YES   | AUTO_INCREMENT |
| genre_name| VARCHAR(255)| NO       | UNIQUE|                |

## program_genre_table (番組ジャンルテーブル)

| フィールド  | データ型   | Null許可 | 主キー | その他 |
|-----------|-----------|----------|-------|-------|
| program_id| BIGINT(20)| NO       | YES   |       |
| genre_id  | BIGINT(20)| NO       | YES   |       |

