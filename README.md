# college-subreddits
An eventually-complete list of college subreddits.

If you notice your college subreddit isn't on this list, feel free to open an issue (or submit a Pull Request)

## Import
```bash
sqlite3 data.db
CREATE TABLE subreddits (name TEXT, location TEXT, subreddit TEXT COLLATE NOCASE);
.separator ','
.import data/colleges.csv subreddits
```

Or at once

```bash
tail -n+2 data/colleges.csv > data.csv && echo -e ".separator ","\nCREATE TABLE subreddits (name TEXT, location TEXT, subreddit TEXT);\n.import data.csv subreddits" | sqlite3 data.db && rm data.csv
```

## Updating
```sql
INSERT INTO subreddits (name, location, subreddit) VALUES ('Langara College', 'langara');
```

## Export

```bash
sqlite3 data.db <<!
.headers on
.mode csv
.output data/colleges.csv
SELECT name, location, subreddit FROM subreddits ORDER BY name ASC;
!
```
