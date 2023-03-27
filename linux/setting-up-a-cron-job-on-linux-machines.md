# Setting up a Cron Job on Linux Machines

A Cron job is a very powerful tool to on Linux machines, and It's easy to set up using the `crontab` command:

```sh
crontab -e
```

This opens a crontab in your text editor, where you can configure a cron job. Here is a quick example to test your cron job:

First, create a Python file:

```py
print("If you can see this, it's working!")
```

Next, add the following test script to cron file:

```sh
* * * * * /usr/bin/python3 /home/josh/test.py >> /home/josh/cron.log
```

This will create a `cron.log` file in your home directory that contains the log content from your Python script.

Here are some more example for cron schedule expressions:

```sh
# Run every 10 minutes
*/10 * * * * /home/josh/my_script.sh

# Run at specific times
# Every day at 5 AM
00 05 * * * cd /home/josh/weather-forecaster && npm run start

# Every day at 7:30 AM
00 07 * * * cd /home/ohara/weather-forecaster && npm run start

# Every day at 20:30 PM
30 20 * * * cd /home/ohara/weather-forecaster && npm run start
```

when setting up the time, it's important to know the timezone your service is running on. To switch timezones, use the following in your crontab file:

```
CRON_TZ=Asia/Taipei
```

Reference:

- [Crontab guru](https://crontab.guru/) - A handy tool for creating and testing your cron schedule expressions
- [Run your web scraper automatically once a day](https://www.youtube.com/watch?v=VztRqRXeyn0&ab_channel=JohnWatsonRooney)
