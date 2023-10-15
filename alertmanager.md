Setup Alertmanager with email notification
### 1. Download alertmanager
```
wget https://github.com/prometheus/alertmanager/releases/download/v0.23.0/alertmanager-0.23.0.linux-amd64.tar.gz
tar xvfz alertmanager-0.23.0.linux-amd64.tar.gz
chmod +x alertmanager
./alertmanager --version
```

### 2. Configure Alertmanager:

- Create an `alertmanager.yml` configuration file.
- Configure the email notification settings in the `alertmanager.yml` file:

  ```yaml
global:
  resolve_timeout: 5m

receivers:
- name: 'email-notifications'
  email_configs:
  - to: 'your-email@example.com'
    from: 'your-gmail-address@gmail.com'
    smarthost: 'smtp.gmail.com:587'
    auth_username: 'your-gmail-address@gmail.com'
    auth_password: 'your-gmail-password'
    send_resolved: true
```

### 3. Start Alertmanager:

- Run the Alertmanager binary, specifying the configuration file:
  ```
  ./alertmanager --config.file=alertmanager.yml
  ```

### 4. Configure Prometheus:

- Update the Prometheus configuration (`prometheus.yml`) to include the Alertmanager configuration:

  ```yaml
  alerting:
    alertmanagers:
    - static_configs:
      - targets:
        - 'localhost:9093'  # Assuming Alertmanager is running on the same machine
  ```

### 5. Test Email Notifications:

- Trigger a test alert in Prometheus to ensure that Alertmanager sends email notifications for the triggered alerts.

Make sure to replace the placeholder values such as email addresses, SMTP server details, and authentication credentials with your actual configuration. Adjust the configurations based on your specific email service provider's requirements.

