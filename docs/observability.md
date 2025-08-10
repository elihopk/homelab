# Observability

Unified metrics and logs across hypervisors and service hosts, deployed by Ansible.

---

## Metrics
- **Hypervisors**: System metrics + device/SMART telemetry.
- **Container hosts**: Container‑level metrics via **cAdvisor**.
- **Central node**: Time‑series storage, dashboards, and alerting with **Prometheus** and **Grafana**.

## Logs
- **Non‑container hosts** forward via **rsyslog** using a templated config.
- **Container hosts** send logs using **Alloy**.
- **Central node** aggregates, stores, presents logs, and issues alerts with **Loki** and **Grafana**.

---

## Deployment
- `monitor` role: central metrics/logs stack (configs + compose).
- Exporters installed on appropriate hosts (system and SMART).
- `templates/rsyslog.conf.j2` applied to forwarders.

---

## Maintenance
- Monitor retention/storage for both metrics and logs.
- Validate scrape/forwarding targets after host changes.
