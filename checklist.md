# Setup Checklist - Grafana Alert Triage Agent

Work through these in order.

Step 1. Import grafana-alert-triage-agent.json into your n8n instance.
Step 2. Attach an Anthropic credential to the Classify Alert AI node.
Step 3. Attach a Slack credential to Post Suppressed Log and Post Escalation.
Step 4. Point both Slack nodes' channelId at your own channel (defaults to alerts-demo).
Step 5. Activate the workflow, copy its production webhook URL.
Step 6. Test with test-payloads.json via curl before wiring a real Grafana instance, see README.
Step 7. In Grafana: Alerting, then Contact points, then New contact point, then Webhook. Paste the n8n webhook URL.
Step 8. Point a Grafana notification policy at the new contact point.
Step 9. Fire a real test alert from Grafana and confirm it lands in Slack.
Step 10. Tune the flap-detection window and threshold in the Flap Check node for your own alert volume.
Step 11. Swap the placeholder Slack channel name and any demo links for your team's real ones before relying on this in production.
