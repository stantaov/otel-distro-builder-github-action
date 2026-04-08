# otel-custom-agent

A custom-built OpenTelemetry Collector distribution tailored for security observability pipelines. It bundles upstream OTel core and contrib components alongside custom exporters for Google Cloud Pub/Sub (with `none` compression support) and Parquet-to-GCS, plus BindPlane processors and extensions for managed agent deployments.

## Architecture

```
Security Sources (Cisco WSA, PingOne, Syslog, etc.)
    --> otel-custom-agent (this collector)
        --> Google Cloud Pub/Sub (googlecloudpubsubexporter)
        --> Google Cloud Storage as Parquet (parquetgcsexporter)
        --> Kafka (kafkaexporter)
        --> Chronicle / SecOps (chronicleexporter)
        --> OTLP endpoints (otlpexporter / otlphttpexporter)
```

## Included Components

### Receivers

| Component | Source | Version |
|---|---|---|
| otlpreceiver | OTel Core | v0.146.0 |
| nopreceiver | OTel Core | v0.146.0 |
| hostmetricsreceiver | OTel Contrib | v0.146.0 |
| syslogreceiver | OTel Contrib | v0.146.0 |
| telemetrygeneratorreceiver | BindPlane | v1.94.2 |

### Exporters

| Component | Source | Version |
|---|---|---|
| debugexporter | OTel Core | v0.146.0 |
| nopexporter | OTel Core | v0.146.0 |
| otlpexporter | OTel Core | v0.146.0 |
| otlphttpexporter | OTel Core | v0.146.0 |
| fileexporter | OTel Contrib | v0.146.0 |
| kafkaexporter | OTel Contrib | v0.146.0 |
| googlecloudpubsubexporter | Custom Fork | v0.146.2 |
| parquetgcsexporter | Custom | v1.0.2 |
| googlecloudstorageexporter | BindPlane | v1.94.2 |
| chronicleexporter | BindPlane | v1.94.2 |
| chronicleforwarderexporter | BindPlane | v1.94.2 |

### Processors

| Component | Source | Version |
|---|---|---|
| batchprocessor | OTel Core | v0.146.0 |
| memorylimiterprocessor | OTel Core | v0.146.0 |
| attributesprocessor | OTel Contrib | v0.146.0 |
| filterprocessor | OTel Contrib | v0.146.0 |
| transformprocessor | OTel Contrib | v0.146.0 |
| resourceprocessor | OTel Contrib | v0.146.0 |
| resourcedetectionprocessor | OTel Contrib | v0.146.0 |
| k8sattributesprocessor | OTel Contrib | v0.146.0 |
| redactionprocessor | OTel Contrib | v0.146.0 |
| tailsamplingprocessor | OTel Contrib | v0.146.0 |
| probabilisticsamplerprocessor | OTel Contrib | v0.146.0 |
| groupbyattrsprocessor | OTel Contrib | v0.146.0 |
| groupbytraceprocessor | OTel Contrib | v0.146.0 |
| logdedupprocessor | OTel Contrib | v0.146.0 |
| spanprocessor | OTel Contrib | v0.146.0 |
| cumulativetodeltaprocessor | OTel Contrib | v0.146.0 |
| deltatorateprocessor | OTel Contrib | v0.146.0 |
| metricsgenerationprocessor | OTel Contrib | v0.146.0 |
| metricstransformprocessor | OTel Contrib | v0.146.0 |
| remotetapprocessor | OTel Contrib | v0.146.0 |
| sumologicprocessor | OTel Contrib | v0.146.0 |
| unrollprocessor | OTel Contrib | v0.146.0 |
| datapointcountprocessor | BindPlane | v1.94.2 |
| logcountprocessor | BindPlane | v1.94.2 |
| lookupprocessor | BindPlane | v1.94.2 |
| maskprocessor | BindPlane | v1.94.2 |
| metricextractprocessor | BindPlane | v1.94.2 |
| metricstatsprocessor | BindPlane | v1.94.2 |
| removeemptyvaluesprocessor | BindPlane | v1.94.2 |
| resourceattributetransposerprocessor | BindPlane | v1.94.2 |
| samplingprocessor | BindPlane | v1.94.2 |
| snapshotprocessor | BindPlane | v1.94.2 |
| spancountprocessor | BindPlane | v1.94.2 |
| throughputmeasurementprocessor | BindPlane | v1.94.2 |
| topologyprocessor | BindPlane | v1.94.2 |

### Extensions

| Component | Source | Version |
|---|---|---|
| zpagesextension | OTel Core | v0.146.0 |
| healthcheckextension | OTel Contrib | v0.146.0 |
| pprofextension | OTel Contrib | v0.146.0 |
| filestorage | OTel Contrib | v0.146.0 |
| dbstorage | OTel Contrib | v0.146.0 |
| basicauthextension | OTel Contrib | v0.146.0 |
| bearertokenauthextension | OTel Contrib | v0.146.0 |
| oauth2clientauthextension | OTel Contrib | v0.146.0 |
| oidcauthextension | OTel Contrib | v0.146.0 |
| sigv4authextension | OTel Contrib | v0.146.0 |
| asapauthextension | OTel Contrib | v0.146.0 |
| headerssetterextension | OTel Contrib | v0.146.0 |
| httpforwarderextension | OTel Contrib | v0.146.0 |
| opampextension | OTel Contrib | v0.146.0 |
| awsproxy | OTel Contrib | v0.146.0 |
| ackextension | OTel Contrib | v0.146.0 |
| jaegerremotesampling | OTel Contrib | v0.146.0 |
| dockerobserver | OTel Contrib | v0.146.0 |
| hostobserver | OTel Contrib | v0.146.0 |
| k8sobserver | OTel Contrib | v0.146.0 |
| jaegerencodingextension | OTel Contrib | v0.146.0 |
| otlpencodingextension | OTel Contrib | v0.146.0 |
| jsonlogencodingextension | OTel Contrib | v0.146.0 |
| zipkinencodingextension | OTel Contrib | v0.146.0 |
| bindplaneextension | BindPlane | v1.94.2 |

### Connectors

| Component | Source | Version |
|---|---|---|
| forwardconnector | OTel Core | v0.146.0 |
| countconnector | OTel Contrib | v0.146.0 |
| datadogconnector | OTel Contrib | v0.146.0 |
| exceptionsconnector | OTel Contrib | v0.146.0 |
| failoverconnector | OTel Contrib | v0.146.0 |
| grafanacloudconnector | OTel Contrib | v0.146.0 |
| roundrobinconnector | OTel Contrib | v0.146.0 |
| routingconnector | OTel Contrib | v0.146.0 |
| servicegraphconnector | OTel Contrib | v0.146.0 |
| spanmetricsconnector | OTel Contrib | v0.146.0 |

## Custom Components

### googlecloudpubsubexporter (fork)

A fork of the upstream OTel Contrib `googlecloudpubsubexporter` that adds support for `none` compression. This is useful when the upstream Pub/Sub topic or downstream consumers do not expect compressed payloads.

- Module: `github.com/stantaov/googlecloudpubsubexporter`
- Version: v0.146.2

### parquetgcsexporter

Converts OTel log records with map-type bodies into Apache Parquet files and uploads them to Google Cloud Storage. Designed for security log pipelines feeding BigQuery external tables via Hive-style time partitioning.

- Module: `github.com/stantaov/parquet-gcs-exporter`
- Version: v1.0.2

Key features:
- Dynamic Parquet schema inference from log record bodies
- Type-aware columns (Int64, Double, Bool, String) with fallback to String for mixed types
- Snappy compression
- Hive-style time-partitioned GCS paths
- Cached GCS client with automatic refresh for Workload Identity Federation (WIF) token rotation
- Built-in observability metrics and skipped-record logging

## CI/CD

The collector is built automatically by GitHub Actions when a version tag is pushed. The pipeline produces artifacts for multiple platforms:

| Platform | Artifact Formats |
|---|---|
| linux/amd64 | `.deb`, `.rpm`, `.apk`, `.tar.gz` |
| linux/arm64 | `.deb`, `.rpm`, `.apk`, `.tar.gz` |
| darwin/arm64 | `.tar.gz` |
| windows/amd64 | `.zip` |

All artifacts are attached to a GitHub Release for the corresponding tag.

### Triggering a new build

```bash
git tag v0.0.11
git push origin v0.0.11
```

## Installation on Linux

### Option 1: Install from .deb package (Debian/Ubuntu)

```bash
# Download the latest release (replace VERSION with the actual tag, e.g., v0.0.11)
VERSION=v0.0.11
curl -LO "https://github.com/stantaov/otel-custom-agent/releases/download/${VERSION}/otel-custom-agent_${VERSION#v}_linux_amd64.deb"

# Install
sudo dpkg -i otel-custom-agent_*_linux_amd64.deb
```

### Option 2: Install from .rpm package (RHEL/CentOS/Fedora)

```bash
VERSION=v0.0.11
curl -LO "https://github.com/stantaov/otel-custom-agent/releases/download/${VERSION}/otel-custom-agent_${VERSION#v}_linux_amd64.rpm"

# Install
sudo rpm -ivh otel-custom-agent_*_linux_amd64.rpm
```

### Option 3: Install from tarball (any Linux)

```bash
VERSION=v0.0.11
curl -LO "https://github.com/stantaov/otel-custom-agent/releases/download/${VERSION}/otel-custom-agent_${VERSION#v}_linux_amd64.tar.gz"

# Extract
sudo tar -xzf otel-custom-agent_*_linux_amd64.tar.gz -C /opt/otel-custom-agent

# Make the binary executable
sudo chmod +x /opt/otel-custom-agent/otel-custom-agent
```

### Post-installation setup

#### 1. Create a configuration file

Create your collector configuration at `/etc/otel-custom-agent/config.yaml`. Below is a minimal example:

```yaml
receivers:
  otlp:
    protocols:
      grpc:
        endpoint: 0.0.0.0:4317
      http:
        endpoint: 0.0.0.0:4318

processors:
  batch:
    send_batch_size: 8192
    timeout: 5s
  memory_limiter:
    check_interval: 1s
    limit_mib: 512

exporters:
  debug:
    verbosity: basic

extensions:
  health_check:
    endpoint: 0.0.0.0:13133

service:
  extensions: [health_check]
  pipelines:
    logs:
      receivers: [otlp]
      processors: [memory_limiter, batch]
      exporters: [debug]
```

#### 2. Create a systemd service

Create the file `/etc/systemd/system/otel-custom-agent.service`:

```ini
[Unit]
Description=OpenTelemetry Custom Collector Agent
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=otel
Group=otel
ExecStart=/opt/otel-custom-agent/otel-custom-agent --config /etc/otel-custom-agent/config.yaml
Restart=on-failure
RestartSec=5s
LimitNOFILE=65536
MemoryMax=1G

# Security hardening
NoNewPrivileges=true
ProtectSystem=full
ProtectHome=true

[Install]
WantedBy=multi-user.target
```

#### 3. Create a dedicated service user

```bash
sudo useradd --system --no-create-home --shell /usr/sbin/nologin otel
```

#### 4. Set directory permissions

```bash
sudo mkdir -p /etc/otel-custom-agent
sudo chown -R otel:otel /etc/otel-custom-agent
sudo chown -R otel:otel /opt/otel-custom-agent
```

#### 5. Enable and start the service

```bash
sudo systemctl daemon-reload
sudo systemctl enable otel-custom-agent
sudo systemctl start otel-custom-agent
```

#### 6. Verify the collector is running

```bash
# Check service status
sudo systemctl status otel-custom-agent

# Check logs
sudo journalctl -u otel-custom-agent -f

# Check health endpoint
curl http://localhost:13133
```

### Uninstall

```bash
# Stop and disable the service
sudo systemctl stop otel-custom-agent
sudo systemctl disable otel-custom-agent
sudo rm /etc/systemd/system/otel-custom-agent.service
sudo systemctl daemon-reload

# Remove files
sudo rm -rf /opt/otel-custom-agent
sudo rm -rf /etc/otel-custom-agent

# Remove user
sudo userdel otel

# Or if installed via package manager:
sudo dpkg -r otel-custom-agent    # Debian/Ubuntu
sudo rpm -e otel-custom-agent     # RHEL/CentOS/Fedora
```

## Building Locally

Prerequisites: Go 1.25+, [OpenTelemetry Collector Builder (ocb)](https://github.com/open-telemetry/opentelemetry-collector/tree/main/cmd/builder)

```bash
# Install ocb
go install go.opentelemetry.io/collector/cmd/builder@v0.146.0

# Build the collector
builder --config manifest.yaml

# The binary is output to ./_build/otel-custom-agent
./_build/otel-custom-agent --config config.yaml
```

## Project Structure

```
otel-custom-agent/
  manifest.yaml           # OTel Collector Builder manifest (component list + versions)
  _build/                 # Build output directory (generated)
    main.go
    components.go
    go.mod / go.sum
    otel-custom-agent     # Compiled binary
  .github/workflows/      # CI/CD pipeline definitions
  README.md
```
