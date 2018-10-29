# Fluentd basics
* All inputs are called `events` and given a tag
* Events are sent to output (plugins)
* Filters can modifiy `events` and are placed before outputs (via `match` tag)
* `labels` can be used to reroute events to a different flow
* `Filters` and `outputs/matchers` are applied in the order they appear in the config file.
