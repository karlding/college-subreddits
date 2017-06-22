# college-subreddits
An eventually-complete list of college subreddits. The [list](https://www.reddit.com/r/college/wiki/faq) at [/r/college](https://www.reddit.com/r/college/) forms the basis for this **college subreddit list**, but since they have a restriction where they'll generally only add new subreddits with >500 subscribers, I created this list. 

If you notice your college subreddit isn't on this list, feel free to open an issue (or submit a Pull Request).

## Import
First strip off the headers in the CSV. Then,

```bash
sqlite3 data.db
CREATE TABLE "subreddits" ( `name` TEXT NOT NULL, `location` TEXT NOT NULL, `subreddit` TEXT NOT NULL COLLATE NOCASE )
.separator ','
.import data/colleges.csv subreddits
```

Or at once

```bash
tail -n+2 data/colleges.csv > data.csv && echo -e ".separator ","\nCREATE TABLE subreddits (name TEXT NOT NULL, location TEXT NOT NULL, subreddit TEXT NOT NULL COLLATE NOCASE);\n.import data.csv subreddits" | sqlite3 data.db && rm data.csv
```

## Updating
```sql
INSERT INTO subreddits (name, location, subreddit) VALUES ('University of Waterloo', 'Waterloo, Ontario, Canada', 'uwaterloo');
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
