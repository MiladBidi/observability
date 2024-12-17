# Prometheus Alerting Scenario

This repository demonstrates a simple Prometheus alerting scenario using Prometheus, Alertmanager, and Node Exporter. 
The setup will trigger an email notification when a specific alert condition is met (e.g., CPU stress test or low disk space).

## Prerequisites

- Docker and Docker Compose installed.
- Prometheus and Alertmanager Docker images.
- Node Exporter running on the target machine for monitoring.
- A Gmail account (or another SMTP service) for email notifications.

Setup Instructions

1. Clone the Repository

Clone the repository to your local machine:

$ git clone https://github.com/<your-username>/prometheus-alerting-scenario.git
$ cd prometheus-alerting-scenario

2. Configure Prometheus

Edit the prometheus.yml file to point to your Node Exporter instance for monitoring.
Add any additional targets if needed.

3. Configure Alertmanager

Edit the alertmanager.yml file to set up email notifications.
Set your Gmail credentials or use App Passwords (recommended).
Replace "smtp_from", "smtp_auth_username", and "smtp_auth_password" with your email credentials.

4. Create Alert Rules

The alerting rule for Prometheus is defined in the alert_rules.yml file.
The alert will trigger when CPU usage is high or disk space is low.

5. Running Prometheus and Alertmanager with Docker

You can run Prometheus and Alertmanager with Docker Compose.

6. Test the Alerts

To test the alerts, you can run a CPU stress test using the stress tool:

$ stress --cpu 2 --timeout 60
This will simulate high CPU usage, and Prometheus should trigger the HighCPUUsage alert after the condition is met for 1 minute.

7. Check Alertmanager

Once the alert fires, check the Alertmanager Web UI at http://<alertmanager-host>:9093/#/alerts to verify that the alert is firing.

If you configured email notifications correctly, you should receive an email at the specified address.

Troubleshooting:

Email not sent?

- Ensure that SMTP credentials are correct.
- Check the Gmail account's security settings (allow "less secure apps" or use an app password).
- Review the Alertmanager logs to identify any errors:
$ docker logs alertmanager

Alert not firing?

- Ensure the Prometheus alert condition is correct.
- Check the Prometheus Web UI (http://<prometheus-host>:9090/alerts) for alert status.
- Verify that the alert rule file is loaded correctly in Prometheus.
