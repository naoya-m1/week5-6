# データベースの作成
以下のクエリでデータベースを作成します。
```
CREATE DATABASE Internet_tv;
```
# データベースの選択
```
USE Internet_tv;
```
# テーブルの作成
以下のクエリで必要なテーブルを作成します。
```
CREATE TABLE channel_table (
    channel_id BIGINT(20) PRIMARY KEY AUTO_INCREMENT,
    channel_name VARCHAR(255) UNIQUE NOT NULL
);

CREATE TABLE program_table (
    program_id BIGINT(20) PRIMARY KEY AUTO_INCREMENT,
    program_title VARCHAR(255) UNIQUE NOT NULL,
    program_description TEXT
);

CREATE TABLE season_table (
    season_id BIGINT(20) PRIMARY KEY AUTO_INCREMENT,
    season_number BIGINT(20),
    program_id BIGINT(20),
    FOREIGN KEY (program_id) REFERENCES program_table(program_id),
    UNIQUE KEY (season_number, program_id)
);

CREATE TABLE episode_table (
    episode_id BIGINT(20) PRIMARY KEY AUTO_INCREMENT,
    episode_number BIGINT(20),
    episode_title VARCHAR(255),
    episode_description TEXT,
    video_length TIME,
    release_date DATE,
    views BIGINT(20) DEFAULT 0,
    season_id BIGINT(20),
    program_id BIGINT(20),
    FOREIGN KEY (season_id) REFERENCES season_table(season_id),
    FOREIGN KEY (program_id) REFERENCES program_table(program_id),
    UNIQUE KEY (episode_number, season_id)
);

CREATE TABLE time_slot_table (
    time_slot_id BIGINT(20) PRIMARY KEY AUTO_INCREMENT,
    start_time DATETIME,
    end_time DATETIME,
    channel_id BIGINT(20),
    episode_id BIGINT(20),
    FOREIGN KEY (channel_id) REFERENCES channel_table(channel_id),
    FOREIGN KEY (episode_id) REFERENCES episode_table(episode_id),
    UNIQUE KEY (channel_id, start_time)
);

CREATE TABLE genre_table (
    genre_id BIGINT(20) PRIMARY KEY AUTO_INCREMENT,
    genre_name VARCHAR(255) UNIQUE NOT NULL
);

CREATE TABLE program_genre_table (
    program_id BIGINT(20),
    genre_id BIGINT(20),
    PRIMARY KEY (program_id, genre_id),
    FOREIGN KEY (program_id) REFERENCES program_table(program_id),
    FOREIGN KEY (genre_id) REFERENCES genre_table(genre_id)
);
```

# サンプルデータの挿入
作成したテーブルにサンプルデータを挿入します。
```
-- Insert into channel_table
INSERT INTO channel_table (channel_name) 
VALUES ('Comedy'), ('Drama'), ('Action');

-- Insert into program_table
INSERT INTO program_table (program_title, program_description) 
VALUES ('Program A', 'This is a description for Program A'), 
       ('Program B', 'This is a description for Program B'), 
       ('Program C', 'This is a description for Program C');

-- Insert into season_table
INSERT INTO season_table (season_number, program_id) 
VALUES (1, 1), (2, 1), (1, 2);

-- Insert into episode_table
INSERT INTO episode_table (episode_number, episode_title, episode_description, video_length, release_date, views, season_id, program_id) 
VALUES (1, 'Episode 1', 'This is a description for Episode 1', '00:30:00', '2023-01-01', 1000, 1, 1),
       (2, 'Episode 2', 'This is a description for Episode 2', '00:45:00', '2023-01-02', 1500, 1, 1),
       (3, 'Episode 3', 'This is a description for Episode 3', '00:40:00', '2023-01-03', 1200, 2, 2);

-- Insert into time_slot_table
INSERT INTO time_slot_table (start_time, end_time, channel_id, episode_id) 
VALUES ('2023-05-21 18:00:00', '2023-05-21 18:30:00', 1, 1),
       ('2023-05-21 19:00:00', '2023-05-21 19:45:00', 2, 2),
       ('2023-05-22 20:00:00', '2023-05-22 20:40:00', 3, 3),
       ('2023-05-23 21:00:00', '2023-05-23 21:45:00', 1, 2),
       ('2023-05-24 22:00:00', '2023-05-24 22:40:00', 2, 3);

-- Insert into genre_table
INSERT INTO genre_table (genre_name) 
VALUES ('Horror'), ('Sci-Fi'), ('Thriller');

-- Insert into program_genre_table
INSERT INTO program_genre_table (program_id, genre_id) 
VALUES (1, 1), (1, 2), (2, 3);

```