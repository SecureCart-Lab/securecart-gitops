# Falco / Falcosidekick Slack secret
The committed values deliberately leave `falcosidekick.config.slack.webhookurl` empty. Do not commit a webhook URL.

For the learning lab, after exporting `SLACK_WEBHOOK_URL` in your EC2 shell, deploy/upgrade Falco with a runtime-only Helm value or configure a Falcosidekick existing Secret according to the chart version you are using. Keep the value in a Kubernetes Secret and keep the command/value out of Git; do not place the webhook in a commit.

Falco itself remains managed by Argo CD. Slack is an optional notification sink and should not be allowed to turn the webhook into Git-managed plaintext.
