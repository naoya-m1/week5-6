1.よく見られているエピソードを知りたいです。エピソード視聴数トップ3のエピソードタイトルと視聴数を取得してください
```
SELECT episode_title, views 
FROM episode_table 
ORDER BY views DESC 
LIMIT 3;

```

2.よく見られているエピソードの番組情報やシーズン情報も合わせて知りたいです。エピソード視聴数トップ3の番組タイトル、シーズン数、エピソード数、エピソードタイトル、視聴数を取得してください

```
SELECT p.program_title, s.season_number, e.episode_number, e.episode_title, e.views
FROM episode_table e
INNER JOIN program_table p ON e.program_id = p.program_id
INNER JOIN season_table s ON e.season_id = s.season_id
ORDER BY e.views DESC 
LIMIT 3;

```

3.本日の番組表を表示するために、本日、どのチャンネルの、何時から、何の番組が放送されるのかを知りたいです。本日放送される全ての番組に対して、チャンネル名、放送開始時刻(日付+時間)、放送終了時刻、シーズン数、エピソード数、エピソードタイトル、エピソード詳細を取得してください。なお、番組の開始時刻が本日のものを本日方法される番組とみなすものとします
```
SELECT 
    channel_table.channel_name,
    time_slot_table.start_time,
    time_slot_table.end_time,
    season_table.season_number,
    episode_table.episode_number,
    episode_table.episode_title,
    episode_table.episode_description
FROM 
    time_slot_table
    INNER JOIN channel_table ON time_slot_table.channel_id = channel_table.channel_id
    INNER JOIN episode_table ON time_slot_table.episode_id = episode_table.episode_id
    INNER JOIN season_table ON episode_table.season_id = season_table.season_id
WHERE 
    DATE(time_slot_table.start_time) = '2023-05-21';
```
4.ドラマというチャンネルがあったとして、ドラマのチャンネルの番組表を表示するために、本日から一週間分、何日の何時から何の番組が放送されるのかを知りたいです。ドラマのチャンネルに対して、放送開始時刻、放送終了時刻、シーズン数、エピソード数、エピソードタイトル、エピソード詳細を本日から一週間分取得してください
```
SELECT 
    channel_table.channel_name,
    time_slot_table.start_time,
    time_slot_table.end_time,
    season_table.season_number,
    episode_table.episode_number,
    episode_table.episode_title,
    episode_table.episode_description
FROM 
    time_slot_table
    INNER JOIN channel_table ON time_slot_table.channel_id = channel_table.channel_id
    INNER JOIN episode_table ON time_slot_table.episode_id = episode_table.episode_id
    INNER JOIN season_table ON episode_table.season_id = season_table.season_id
WHERE 
    channel_table.channel_name = 'Drama' 
    AND DATE(time_slot_table.start_time) BETWEEN '2023-05-21' AND DATE_ADD('2023-05-21', INTERVAL 7 DAY);

```
3,4に関しては、2023-05-21の部分に都度当日の日付を入れる
