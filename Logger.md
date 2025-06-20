I used to use print statements to debug, now I have switched to using Loggers and it has made debugging cleaner and fun! 

`logger` is a dart package that prints formatted logs with different levels (trace, debug, info, warning, error, fatal) and customizes the output through a PrettyPrinter. My info logs are highlighted with emojis and colors, which makes it easier for me to read my debug logs in console.


Some core concepts related to logger:

- You can use methods like logger.t(), logger.d(), logger.i(), logger.w(), logger.e(), and logger.f() to log messages at different levels (trace, debug, info, warning, error, fatal). You can pass string, list, set, maps etc in the logger instance.

- Control which logs to show using `LogFilter`

- Control where logs are sent using `LogOutput`

You can learn more about this in the following link:

- [Logger package official documentation](https://pub.dev/packages/logger)
