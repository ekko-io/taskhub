# Taskhub

A system for executing scheduled tasks (cron) and manual tasks
(web/rest/webhook).

Features:

* Manual task execution
* Crontab-like scheduled task execution
* Webhook task execution
* Tasks can be in any programming language
* Reporting of task executions via UI and Rest services
* Push of task status (webhook or other kind of notifications)
* Docker-based task exececution


## Manual execution

Manual execution is triggered using REST services. This is the base for all other
methods of execution (scheduling and webhook).

A task is associated with a user, repository and a name. One user can have multiple
repositories (github or other git hosts) and each repository can have multiple tasks. To
trigger a task, you can execute the following GET or POST request:

```
/trigger/<user>/<repo>/<name>
```

For example:

```
POST /trigger/srs/mytasks/send-mail
```

If you want to send parameters to a task, http query parameters are used:

```
GET /trigger/srs/mytasks/send-mail?to=someone@foo.bar
```


## WebHook execution

WebHook execution is triggering a task on a certain webhook. This is a seperate
endpoint (/webhook) and should follow a specified protocol. In the end it will
trigger a task using the REST interfaces.


## Scheduled execution

We need a scheduler that is clustered. This scheduler is only used for executing
REST requests to trigger execution.


## Diagrams

![API Diagram](https://rawgithub.com/ekko-io/taskhub/master/images/api.svg)
