# tg-feed-bot

The tg-feed-bot is telegram bot to notify a channel whenever a new post appears in an RSS/Atom Feed.

## How does it work?

A Python script is run periodically (typically via cron) and it reads an RSS/Atom feed and sends notifications for all the new posts. It maintains a list of posts that it has already seen in a [dbm][] database.

[dbm]: https://docs.python.org/3/library/dbm.html

The url of the feed and telegram channel are specified in a config file.

## Configuration

The tg-feed-bot using a JSON config file. A sample config file with name `sample_config.json` is provided in the repository.

```
$ cat sample_config.json
{
    "feed_url": "https://example.com/feed.rss",
    "db_path": "tg-feed-bot.db",
    "telegram_token": "9876543210:ABCDEFGHIJKLMNOPQRSTU-XYZ0123456789",
    "chat_id": -12345678,
    "message_prefix": "New Post in the blog:"
}
```

Please copy `sample_config.json` to `config.json` and edit that file before running the `feedbot.py`.

Here is the explanation of each of the fields in the config file.

* **feed_url**: The URL of the RSS/Atom feed
* **db_path**: path to a file in the file system where `tg-feed-bot` will remember the already seen urls
* **telegram_token**: API token for your telegram bot
* **chat_id**: id of the telegram channel to send the message
* **message_prefix**: The prefix to use to construct the message, the default value is "New post:"

## How to run

Before you can run the program you need to install the dependencies. It is recommended to use a virtualenv.

```
$ python3 -m venv venv
$ . venv/bin/activate
$ pip install -r requirements.txt
```

Make sure the `config.json` is setup (see the previous section for instructions).

After preparing the `config.json`, run the `feedbot.py`

```
$ python feedbot.py
```

This will run and sends notifications to all the new entries that it sees in the feed.

You may want to configure a cron job to run this periodically.

## License

This software is licensed under MIT license.
