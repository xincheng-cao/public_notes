## daemon
`pkill gunicorn`

Use --daemon option while running gunicorn. Example:

`gunicorn grand56.wsgi:application --name grand56 --workers 3 --user=root --group=root --bind=127.0.0.1:1001 --daemon`

## logging
- superset event logging
    - Superset by default logs special action events in its internal database. These logs can be accessed on the UI by navigating to Security > Action Log. You can freely customize these logs by implementing your own event log class.
- superset StatsDlogging
    - Superset can be instrumented to log events to StatsD if desired. Most endpoints hit are logged as well as key events like query start and end in SQL Lab.(to-do)

### errorlog

Command line: `--error-logfile FILE` or `--log-file FILE`

Default: '-'

The Error log file to write to.

***Using '-' for FILE makes gunicorn log to stderr.***

Changed in version 19.2: Log to stderr by default.

*can use this technique to send log to a file instad of stderr so you can use tail to monitor the error logs*

`gunicorn       -w 10       -k gevent       --timeout 120       -b  0.0.0.0:8088       --limit-request-line 0       --limit-request-field_size 0       "superset.app:create_app()" --daemon --log-file ~/superset.log`

capture_output
Command line: `--capture-output`

Default: False

Redirect stdout/stderr to specified file in errorlog.

`gunicorn       -w 10       -k gevent       --timeout 120       -b  0.0.0.0:8088       --limit-request-line 0       --limit-request-field_size 0       "superset.app:create_app()" --daemon --capture-output --log-file ~/superset.log`