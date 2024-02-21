# spectrum_virtualize_exporter

Prometheus exporter for IBM Spectrum Virtualize (e.g. Storwize V7000).

# Dashboard

Works with the [Grafana
Dashboard](https://grafana.com/grafana/dashboards/13753-v7000/) by the
[original author](https://github.com/bluecmd/spectrum_virtualize_exporter)

# Supported Metrics

 * `spectrum_power_watts`
 * `spectrum_temperature`
 * `spectrum_drive_status`
 * `spectrum_psu_status`
 * `spectrum_pool_capacity_bytes`
 * `spectrum_pool_free_bytes`
 * `spectrum_pool_status`
 * `spectrum_pool_used_bytes`
 * `spectrum_pool_volume_count`
 * `spectrum_node_compression_usage_ratio`
 * `spectrum_node_fc_bps`
 * `spectrum_node_fc_iops`
 * `spectrum_node_iscsi_bps`
 * `spectrum_node_iscsi_iops`
 * `spectrum_node_sas_bps`
 * `spectrum_node_sas_iops`
 * `spectrum_node_system_usage_ratio`
 * `spectrum_node_total_cache_usage_ratio`
 * `spectrum_node_write_cache_usage_ratio`
 * `spectrum_node_mdisk_read_iops`
 * `spectrum_node_mdisk_write_iops`
 * `spectrum_node_mdisk_read_ms`
 * `spectrum_node_mdisk_write_ms`
 * `spectrum_node_mdisk_read_mb`
 * `spectrum_node_mdisk_write_mb`
 * `spectrum_fc_port_speed_bps`
 * `spectrum_fc_port_status`
 * `spectrum_ip_port_link_active`
 * `spectrum_ip_port_speed_bps`
 * `spectrum_ip_port_state`

## Usage

Example:

```
./spectrum_virtualize_exporter \
  -auth-file ~/spectrum-monitor.yaml \
  -extra-ca-cert ~/namecheap.ca.crt
```

Where `~/spectrum-monitor.yaml` contains pairs of Spectrum targets
and login information in the following format:

```
"https://my-v7000:7443":
  user: monitor
  password: passw0rd
"https://my-other-v7000:7443":
  user: monitor2
  password: passw0rd1
```

The flag `-extra-ca-cert` is useful as it appears that at least V7000 on the
8.2 version is unable to attach an intermediate CA.

Prometheus configuration can look like this:

```
  - job_name: 'StorWize'
    metrics_path: /probe
    static_configs:
      - targets: ['localhost:9747']
    params:
      target: ['https://my-v7000:7443']
```

## Repo info
This is a fork of trappiz `spectrum_virtualize_exporter`, which is a fork of
bluecmd `spectrum_virtualize_exporter`. Just fixed JSON number handling.

