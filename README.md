# Grafana Alert Triage Agent

Free n8n template from the Survives Production YouTube channel (youtube.com/@survivesproduction).

An AI agent that sits between Grafana Alerting and Slack. It reads every alert, remembers how often that exact alert has fired recently (flap detection), and only escalates the ones that actually need a human, instead of paging you for every noisy blip.

## What it does

1. Webhook receives Grafana's alerting webhook payload.
2. 2. Parse Grafana Alert flattens the payload into alertname, severity, service, summary, status, dashboardURL, fingerprint.
   3. 3. Flap Check counts how many times this exact alert has fired in the last 10 minutes, using workflow static data as memory.
      4. 4. Classify Alert AI, an Anthropic Claude call, decides noise vs real given the alert's context and recent fire count.
         5. 5. Route by decision sends noise alerts to a quiet logged Slack message and real alerts to an urgent escalation with a link to the Grafana dashboard.
           
            6. ## Setup
           
            7. 1. Import grafana-alert-triage-agent.json into n8n.
               2. 2. Add your Anthropic credential to the Classify Alert AI node.
                  3. 3. Add your Slack credential to both Slack nodes and point channelId at your own alerts channel, defaults to alerts-demo.
                     4. 4. Activate the workflow and copy the webhook production URL.
                        5. 5. In Grafana: Alerting, then Contact points, then New contact point, then Webhook. Paste the n8n webhook URL, then point a notification policy at it.
                          
                           6. No live Grafana instance? Use test-payloads.json to fire simulated alerts at the webhook with curl.
                          
                           7. ## Flap-detection window
                          
                           8. Default: an alert fired 4 or more times in the last 10 minutes is treated as noise unless severity is critical. Tune the threshold in the Flap Check code node.
                          
                           9. ## Notes
                          
                           10. This is a public template. The demo Slack channel name and links are placeholders, swap them for your own before using in production. Credentials are never included in the exported workflow JSON. Full build walkthrough on the Survives Production YouTube channel.
