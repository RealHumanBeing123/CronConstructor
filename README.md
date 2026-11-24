# CronConstructor

Like cURL Craft & wget wizard, but for cron schedules, and still offline. The HTML file is all that you need.

Build a cron schedule by clicking, or paste one you already have to see it in plain English and find out when it runs next. Nothing is sent anywhere: the page makes no network requests.

How it works:
- The expression box at the top is editable. Type or paste an expression and the builder below follows it. Change the builder and the expression updates. Names such as `MON-FRI` and `JAN,JUL`, and shortcuts such as `@daily`, `@weekly` and `@reboot`, are understood.
- Each field (minute, hour, day of month, month, day of week) can be set to every value, every N, between two values (with an optional step), specific values picked from buttons, or custom text for anything unusual.
- A plain-English description updates as you go, for example "Every 15 minutes, between 9:00 AM and 5:59 PM, on Monday through Friday".

Beyond the builder itself, I added a few more things:

- Next runs: the next 10 times the schedule fires, with how long until each one. Times can be shown in your time zone or UTC, in 12-hour or 24-hour form. Only schedules that actually occur are listed, so an impossible date such as February 30 shows no runs.

- What each part does: a table that breaks the expression into fields and says what each one means.

- Crontab line: add your command and get a complete line to paste into `crontab -e`. It can discard or log the output, stop overlapping runs with `flock`, set `MAILTO`, `PATH` and `SHELL=/bin/bash`, add a comment and a user column for `/etc/cron.d`. Any `%` in your command is escaped for you, because cron treats a bare `%` as a line break.

- Quick-start recipes: 19 examples such as every 5 minutes, weekdays at 9 AM, the first of the month, every quarter, weekends, and when the system starts.

- 6-field mode: an optional seconds field for schedulers that use it, such as Spring or node-cron.

- Warnings: for a schedule where both day-of-month and day-of-week are set (standard cron runs on either one, not both), steps that don't divide evenly (such as every 7 minutes, where the gap shrinks each hour), days that don't exist in some months (day 31), schedules that never run, jobs around 1 to 3 AM that daylight saving time can skip or repeat, and very frequent schedules.

- Clear errors: for steps larger than the field, a range written backwards, `L`, `W` and `#` (which only Quartz-style schedulers support), and the wrong number of fields.

Run times were checked against the `croniter` library on 1,500 random schedules with no differences. One deliberate difference: like the real Linux cron, a day field written as `*/n` counts as "every day", so it combines with the other day field using AND rather than OR.

It follows standard Linux and macOS cron (Vixie/cronie) rules. Quartz-only features and a year field are not supported. The page shows times on your computer's clock, while a real job uses the time zone of the machine it runs on.

Just open `CronConstructor.html` in any browser. It works with no internet connection.

<img width="742" height="974" alt="cron" src="https://github.com/user-attachments/assets/b064d1cf-6e1c-4284-bbd5-71ae44a42b5e" />
