# prometheus-demo

Local [Prometheus](https://prometheus.io) + [Grafana](https://grafana.com) monitoring stack running inside [DDEV](https://ddev.readthedocs.io).

Provided by [Christian Spoo](https://github.com/cspoo) at [Marketing Factory Digital GmbH](https://www.marketing-factory.de) as a demo stack for local development. **We are unable to provide support for this setup.**

---

## What's included

| Service    | URL                                        | Credentials      |
|------------|--------------------------------------------|------------------|
| Prometheus | https://prometheus-demo.ddev.site:9090     | —                |
| Grafana    | https://prometheus-demo.ddev.site:3000     | `admin` / `grafana` |

Grafana is pre-provisioned with Prometheus as its default datasource. Anonymous access is enabled with Admin role, so no login is required for local use.

## Prerequisites

- [DDEV](https://ddev.readthedocs.io/en/stable/users/install/) v1.22+

## Getting started

```bash
# Clone the repo
git clone https://github.com/marketing-factory/prometheus-demo.git
cd prometheus-demo

# Add your scrape targets (see below)
$EDITOR .ddev/prometheus/prometheus.yml

# Start the stack
ddev start
```

Open Grafana at https://prometheus-demo.ddev.site:3000.

## Configuring scrape targets

Edit `.ddev/prometheus/prometheus.yml` and add your targets under `scrape_configs`:

```yaml
scrape_configs:
  - job_name: prometheus
    tls_config:
      insecure_skip_verify: true   # required for DDEV's self-signed certs
    static_configs:
      - targets:
          - example.ddev.site       # replace with your DDEV project hostname
```

Restart Prometheus after changes:

```bash
ddev restart
```

## Stopping the stack

```bash
ddev stop
```

Prometheus time-series data persists in a named Docker volume (`prom_data`) across restarts.

---

## About

[Marketing Factory Digital GmbH](https://www.marketing-factory.de) is a Düsseldorf-based agency specialising in TYPO3 and Shopware enterprise solutions, API integrations, and long-term digital partnerships.

This repository is published as-is for demo and educational purposes. No warranty is provided.
