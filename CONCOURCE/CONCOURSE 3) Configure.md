# CONCOURSE CONFIGURATION

[Tutorial](https://concoursetutorial.com/)

## TARGET

In the spirit of declaring absolutely everything you do to get absolutely the same result every time, the fly CLI requires that you specify the target API for every `fly` request.

For example, alias it with a name `tutorial` (this name is used by all the tutorial task scripts).
```
fly --target tutorial login --concourse-url http://127.0.0.1:8080 -u admin -p admin
fly --target tutorial sync
```

































