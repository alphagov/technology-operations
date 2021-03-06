### Create and edit alerts using Prometheus

When deciding what alerts you want to receive, consider:

- reading the [Alerting principles][6] in the GDS Way
- looking at [existing alerting rules][2] used by other GDS teams
- talking to us for advice using the [#re-prometheus-support][7] Slack channel

### How to create or update alerting rules

You should first read [Prometheus' alerting rules documentation][4] to understand how alerting works.

You will also need to understand how to write an expression in [PromQL][5] for your alerting rules.

### Writing your alerting rule PromQL expression

Use the [Prometheus dashboard][1] to experiment writing your alert as a [PromQL][5] expression.

Your expression must contain an `org` label, which refers to your PaaS organisation. This makes you sure it only uses metrics from your team. Although you can use the `job` label for this, it is not guaranteed to be unique to your team.

You should only include timeseries for the PaaS space you wish to alert on, for example only including production using the `space="production"` label.

### Create the alerting rule

Alerting rules are defined in YAML format in a config file in the [prometheus-aws-configuration-beta][2] repository. Each product team should use their own file for their alerting rules.

Alerting rules should be prefixed with your team name, for example `registers_RequestsExcess5xx` or `DGU_HighDiskUsage`. This makes your alert easier to identify.

You must add a `product` label to your alerting rule under `labels` so if the alert is triggered, Prometheus will alert the correct team.

The alerting rule file should look something like this:

```
groups:
- name: Your team name
  rules:
  - alert: TeamName_RequestsExcess5xx
    expr: rate(requests{org="your-paas-org", job="yourteam-metric-exporter", space="prod", status_range="5xx"}[5m]) > 1
    for: 120s
    labels:
        product: "yourteam"
    annotations:
        summary: "App {{ $labels.app }} has too many 5xx errors"
        description: "Further context to help your fix this alert. You should include a link to your runbook for this alert if you have one"
        logs: "A link to any relevant logs, for example https://kibana.logit.io/s/<stack-id>/app/kibana#/discover?_g=()"
        dashboard: "A link to any relevant monitoring dashboards, for example https://grafana-paas.cloudapps.digital/d/<dashboard-id>"
```

You may have to iterate your alerting rules to make them more useful for your team. For example you may get alerts that did not require any action as the threshold was too low.

### Create a PR with your alerting rule

Create a pull request for changes to your alerting rules file. Your commit should explain what the alert is and why you picked the threshold value. This is so future team members have the context they need to confidently change the alerting rule and other teams can learn from your alerting rules.

Share your pull request in the [#re-prometheus-support Slack channel][7] channel so we can review it. We will try to merge and deploy your pull request as quickly as possible and will let you know when your alerting rule is live.

### How to receive alerts

Once Prometheus triggers an alert, it sends the alert to [Alertmanager][10]. Alertmanager is then responsible for forwarding alerts to receivers such as [Pagerduty][11] or [Zendesk][12].

Alerts are forwarded to the appropriate team and receiver using the [Alertmanager config file][9] which uses the alert labels to direct the alert to the right team and receiver.

If you have not yet set up a receiver or would like to set up additional receivers use the [#re-prometheus-support Slack channel][7].


[0]: https://prometheus.io/
[1]: https://prom-2.monitoring.gds-reliability.engineering
[2]: https://github.com/alphagov/prometheus-aws-configuration-beta/tree/master/terraform/projects/app-ecs-services/config/alerts
[3]: https://github.com/alphagov/prometheus-aws-configuration-beta/
[4]: https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/
[5]: https://prometheus.io/docs/prometheus/latest/querying/basics/
[6]: https://gds-way.cloudapps.digital/standards/alerting.html#alerting
[7]: https://gds.slack.com/messages/re-prometheus-support
[8]: https://github.com/alphagov/paas-metric-exporter
[9]: https://github.com/alphagov/prometheus-aws-configuration-beta/blob/master/terraform/projects/app-ecs-services/templates/alertmanager.tpl
[10]: https://prometheus.io/docs/alerting/alertmanager/
[11]: https://www.pagerduty.com/
[12]: https://www.zendesk.com/
