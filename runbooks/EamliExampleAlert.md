# EamliExampleAlert

* ENDPOINT: X
* SERVICE: Y
* TRACE ID: 123abc

## Description

The `EamliExampleAlert` is triggered when the X endpoint for service Y returns a 500 response.

## Impact

### Customer

Customers attempting to hit this endpoint will see an error message, and could be prevented from using some functionality of the eamli service.

## Diagnosis

### Upstream Services

This endpoint depends on the database to perform user lookups.

## Mitigation

All 500 errors result in a stack trace log being generated. Use the trace ID of this alert to identify the request via the logs, and inspect the stack trace message to gather further information about the issue.

## Further insights

### Related Logs

Using your log storage solution, search of all logs at the X endpoint, for service Y, with the `traceID` value of `123abc`

### Prometheus query

This alert is triggered by events from this PromQL query:

`/prometheus/graph?g0.expr=rate(eamli_http_request_duration_count%7Bpath%3D%22X%22%2C%20service%3D%22Y%22%2C%20status_code%3D%22500%22%7D%5B1m%5D)&g0.tab=0&g0.stacked=0&g0.show_exemplars=0&g0.range_input=1h`

### Grafana Dashboard

See the eamli RED dashboard for an overview of the service requests

`/grafana/d/cwxQ7ZL7z/eamli-red`
