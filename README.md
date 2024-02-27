# redisJobRunnerService

**Continuously process a MediaWiki jobqueue**

## Description

`redisJobRunnerService` is an infinite "while loop" used to call MediaWiki `runJobs.php` and eventually attempt to process any job enqueued. A number of virtual sub-loops with their own runners and job types must be defined via parameters. These loops can set any of the job types as either low or high priority. High priority will get ~80% of the time share of the sub-loop under "busy" conditions. If there are few high priority jobs, the loops will spend much more of their time on the low priority ones.

The runner must be started with a config file location specified. An annotated example config file is provided in `jobrunner.sample.json`. You will probably want to run this script under your webserver username. The runner can be made into a service via upstart (or anything comparable).

Example:
```
redisJobRunnerService --config-file=/etc/jobrunner/jobrunner.json --verbose
```

## License

GPLv3.0, see [LICENSE.md](LICENSE.md) for the complete license.
