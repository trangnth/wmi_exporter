# service collector

The service collector exposes metrics about Windows Services

|||
-|-
Metric name prefix  | `service`
Classes             | [`Win32_Service`](https://msdn.microsoft.com/en-us/library/aa394418(v=vs.85).aspx)
Enabled by default? | Yes

## Flags

### `--collector.service.services-where`

A WMI filter on which services to include. Recommended to keep down number of returned metrics.

Example: `--collector.service.services-where="Name='wmi_exporter'"`

## Metrics

Name | Description | Type | Labels
-----|-------------|------|-------
`wmi_service_state` | The state of the service, 1 if the current state, 0 otherwise | gauge | name, state
`wmi_service_start_mode` | The start mode of the service, 1 if the current start mode, 0 otherwise | gauge | name, start_mode
`wmi_service_status` | The status of the service, 1 if the current status, 0 otherwise | gauge | name, status

For the values of the `state`, `start_mode` and `status` labels, see below.

### States

A service can be in the following states:
- `stopped`
- `start pending`
- `stop pending`
- `running`
- `continue pending`
- `pause pending`
- `paused`
- `unknown`

### Start modes

A service can have the following start modes:
- `boot`
- `system`
- `auto`
- `manual`
- `disabled`

### Status

A service can have any of the following statuses:
- `ok`
- `error`
- `degraded`
- `unknown`
- `pred fail`
- `starting`
- `stopping`
- `service`
- `stressed`
- `nonrecover`
- `no contact`
- `lost comm`

Note that there is some overlap with service state.

### Example metric
_This collector does not yet have explained examples, we would appreciate your help adding them!_

* Start mode

```sh
wmi_service_start_mode{name="adobeupdateservice",start_mode="auto"} 1
wmi_service_start_mode{name="adobeupdateservice",start_mode="boot"} 0
wmi_service_start_mode{name="adobeupdateservice",start_mode="disabled"} 0
wmi_service_start_mode{name="adobeupdateservice",start_mode="manual"} 0
wmi_service_start_mode{name="adobeupdateservice",start_mode="system"} 0
wmi_service_start_mode{name="agmservice",start_mode="auto"} 1
wmi_service_start_mode{name="agmservice",start_mode="boot"} 0
wmi_service_start_mode{name="agmservice",start_mode="disabled"} 0
wmi_service_start_mode{name="agmservice",start_mode="manual"} 0
wmi_service_start_mode{name="agmservice",start_mode="system"} 0
wmi_service_start_mode{name="agsservice",start_mode="auto"} 1
wmi_service_start_mode{name="agsservice",start_mode="boot"} 0
wmi_service_start_mode{name="agsservice",start_mode="disabled"} 0
wmi_service_start_mode{name="agsservice",start_mode="manual"} 0
```

* State

```sh
wmi_service_state{name="dhcp",state="continue pending"} 0
wmi_service_state{name="dhcp",state="pause pending"} 0
wmi_service_state{name="dhcp",state="paused"} 0
wmi_service_state{name="dhcp",state="running"} 1
wmi_service_state{name="dhcp",state="start pending"} 0
wmi_service_state{name="dhcp",state="stop pending"} 0
wmi_service_state{name="dhcp",state="stopped"} 0
wmi_service_state{name="dhcp",state="unknown"} 0
```

* Status

```sh
wmi_service_status{name="dhcp",status="degraded"} 0
wmi_service_status{name="dhcp",status="error"} 0
wmi_service_status{name="dhcp",status="lost comm"} 0
wmi_service_status{name="dhcp",status="no contact"} 0
wmi_service_status{name="dhcp",status="nonrecover"} 0
wmi_service_status{name="dhcp",status="ok"} 1
wmi_service_status{name="dhcp",status="pred fail"} 0
wmi_service_status{name="dhcp",status="service"} 0
wmi_service_status{name="dhcp",status="starting"} 0
wmi_service_status{name="dhcp",status="stopping"} 0
wmi_service_status{name="dhcp",status="stressed"} 0
wmi_service_status{name="dhcp",status="unknown"} 0
```

## Useful queries
_This collector does not yet have any useful queries added, we would appreciate your help adding them!_

```sh
wmi_service_start_mode{exported_instance="192.168.20.162:9182",exported_job="exporter_win10",instance="192.168.20.162:9091",job="pushgateway_win2",name="adobeupdateservice",start_mode="auto"}
```

## Alerting examples
_This collector does not yet have alerting examples, we would appreciate your help adding them!_
