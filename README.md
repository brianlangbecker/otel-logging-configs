# OpenTelemetry Logging Configurations

A collection of structured log parsing examples and tools for testing with OTTL.run and creating Honeycomb derived columns.

## Overview

This project provides:

- JSON examples for testing with OTTL.run
- Structured log parsing patterns for various log formats
- Honeycomb derived column examples
- Ready-to-use regex patterns for log field extraction

## Structure

```
otel-logging-configs/
├── configs/
│   └── basic-collector.yaml    # Main configuration with log parsing
├── nginx-log-example.json     # OTTL.run example for nginx logs
├── systemd-log-example.json   # OTTL.run example for systemd logs
├── loki-log-example.json      # OTTL.run example for loki logs
└── README.md
```

## Log Formats Supported

### 1. Nginx Access Logs

- HTTP access log format with IP, method, path, status, user agent
- Extracts fields: `http_ip`, `http_method`, `http_path`, `http_status`, `http_user_agent`

### 2. Systemd Journal Logs

- JSON format with errno, priority, and entry message
- Extracts fields: `errno`, `log_priority`, `log_entry`, `transport`

### Common Fields

Both formats include: `app`, `cluster`, `component`, `job`, `namespace`, `node_name`, `pod`, `severity`, `severity_code`

## Usage

### Test with OTTL.run

Use the provided JSON examples to test OTTL expressions at [ottl.run](https://ottl.run):

- **nginx-log-example.json** - Test nginx access log parsing
- **systemd-log-example.json** - Test systemd journal log parsing
- **loki-log-example.json** - Test loki distributed log parsing

## OTTL Transform Examples

Based on the `basic-collector.yaml` transform processor, here are OTTL expressions you can test using the ngnix json file at [ottl.run](https://ottl.run/#eyJ2ZXJzaW9uIjoidjAuMTI4LjAiLCJldmFsdWF0b3IiOiJ0cmFuc2Zvcm1fcHJvY2Vzc29yIiwicGF5bG9hZCI6IntcInJlc291cmNlTG9nc1wiOlt7XCJyZXNvdXJjZVwiOntcImF0dHJpYnV0ZXNcIjpbe1wia2V5XCI6XCJzZXJ2aWNlLm5hbWVcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcIm1pbWlyLW5naW54XCJ9fV19LFwic2NvcGVMb2dzXCI6W3tcImxvZ1JlY29yZHNcIjpbe1widGltZVVuaXhOYW5vXCI6XCIxNzE5MTczMjQwMDAwMDAwMDAwXCIsXCJib2R5XCI6e1wic3RyaW5nVmFsdWVcIjpcImFwcDptaW1pclxcbmJvZHk6MTcyLjE2Ljc0LjkzIC0gLSBbMjMvSnVuLzIwMjU6MjA6MTk6MDggKzAwMDBdIDIwMCBcXFwiUE9TVCAvYXBpL3YxL3B1c2ggSFRUUC8xLjFcXFwiIDAgXFxcIi1cXFwiIFxcXCJQcm9tZXRoZXVzLzIuNTQuMFxcXCIgXFxcIi1cXFwiXFxuY2x1c3Rlcjpzb3gyLXVzZTJcXG5jb21wb25lbnQ6bmdpbnhcXG5jb250YWluZXI6bmdpbnhcXG5maWxlbmFtZTovdmFyL2xvZy9wb2RzL3NlZXEtb2JzZXJ2YWJpbGl0eV9taW1pci1uZ2lueC03NTc4ZDlkYzc1LTR4dDhuXzg4ZGIwMGQ4LTBlM2EtNDBkMC1iNTQ0LTAzMzM1YjJmMDczZi9uZ2lueC8wLmxvZ1xcbmZsYWdzOjBcXG5pbnN0YW5jZTptaW1pclxcbmpvYjpzZWVxLW9ic2VydmFiaWxpdHkvbWltaXJcXG5tZXRhLnNpZ25hbF90eXBlOmxvZ1xcbm5hbWVzcGFjZTpzZWVxLW9ic2VydmFiaWxpdHlcXG5ub2RlX25hbWU6aXAtMTcyLTE2LTY3LTQ3LnVzLWVhc3QtMi5jb21wdXRlLmludGVybmFsXFxucG9kOm1pbWlyLW5naW54LTc1NzhkOWRjNzUtNHh0OG5cXG5TYW1wbGUgUmF0ZToxXFxuc2V2ZXJpdHk6dW5zcGVjaWZpZWRcXG5zZXZlcml0eV9jb2RlOjBcXG5zdHJlYW06c3RkZXJyXFxuLS0tXCJ9LFwiYXR0cmlidXRlc1wiOlt7XCJrZXlcIjpcImFwcFwiLFwidmFsdWVcIjp7XCJzdHJpbmdWYWx1ZVwiOlwibWltaXJcIn19LHtcImtleVwiOlwiYm9keVwiLFwidmFsdWVcIjp7XCJzdHJpbmdWYWx1ZVwiOlwiMTcyLjE2Ljc0LjkzIC0gLSBbMjMvSnVuLzIwMjU6MjA6MTk6MDggKzAwMDBdIDIwMCBcXFwiUE9TVCAvYXBpL3YxL3B1c2ggSFRUUC8xLjFcXFwiIDAgXFxcIi1cXFwiIFxcXCJQcm9tZXRoZXVzLzIuNTQuMFxcXCIgXFxcIi1cXFwiXCJ9fSx7XCJrZXlcIjpcImNsdXN0ZXJcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcInNveDItdXNlMlwifX0se1wia2V5XCI6XCJjb21wb25lbnRcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcIm5naW54XCJ9fSx7XCJrZXlcIjpcImNvbnRhaW5lclwiLFwidmFsdWVcIjp7XCJzdHJpbmdWYWx1ZVwiOlwibmdpbnhcIn19LHtcImtleVwiOlwiZmlsZW5hbWVcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcIi92YXIvbG9nL3BvZHMvc2VlcS1vYnNlcnZhYmlsaXR5X21pbWlyLW5naW54LTc1NzhkOWRjNzUtNHh0OG5fODhkYjAwZDgtMGUzYS00MGQwLWI1NDQtMDMzMzViMmYwNzNmL25naW54LzAubG9nXCJ9fSx7XCJrZXlcIjpcImZsYWdzXCIsXCJ2YWx1ZVwiOntcImludFZhbHVlXCI6XCIwXCJ9fSx7XCJrZXlcIjpcImluc3RhbmNlXCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJtaW1pclwifX0se1wia2V5XCI6XCJqb2JcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcInNlZXEtb2JzZXJ2YWJpbGl0eS9taW1pclwifX0se1wia2V5XCI6XCJtZXRhLnNpZ25hbF90eXBlXCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJsb2dcIn19LHtcImtleVwiOlwibmFtZXNwYWNlXCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJzZWVxLW9ic2VydmFiaWxpdHlcIn19LHtcImtleVwiOlwibm9kZV9uYW1lXCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJpcC0xNzItMTYtNjctNDcudXMtZWFzdC0yLmNvbXB1dGUuaW50ZXJuYWxcIn19LHtcImtleVwiOlwicG9kXCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJtaW1pci1uZ2lueC03NTc4ZDlkYzc1LTR4dDhuXCJ9fSx7XCJrZXlcIjpcIlNhbXBsZSBSYXRlXCIsXCJ2YWx1ZVwiOntcImludFZhbHVlXCI6XCIxXCJ9fSx7XCJrZXlcIjpcInNldmVyaXR5XCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJ1bnNwZWNpZmllZFwifX0se1wia2V5XCI6XCJzZXZlcml0eV9jb2RlXCIsXCJ2YWx1ZVwiOntcImludFZhbHVlXCI6XCIwXCJ9fSx7XCJrZXlcIjpcInN0cmVhbVwiLFwidmFsdWVcIjp7XCJzdHJpbmdWYWx1ZVwiOlwic3RkZXJyXCJ9fV19XX1dfV19IiwiY29uZmlnIjoiZXJyb3JfbW9kZTogaWdub3JlXG5sb2dfc3RhdGVtZW50czpcbiAgICAtIGNvbnRleHQ6IGxvZ1xuICAgICAgc3RhdGVtZW50czpcbiAgICAgICAgICAjIFBhcnNlIEhUVFAgYWNjZXNzIGxvZyBmcm9tIGJvZHkgYXR0cmlidXRlIChhbHJlYWR5IGV4dHJhY3RlZCBmcm9tIGJvZHk6IGtleS12YWx1ZSBwYWlyKVxuICAgICAgICAgICMgRXhhbXBsZSBib2R5IGF0dHJpYnV0ZTogMTcyLjE2Ljc0LjkzIC0gLSBbMjMvSnVuLzIwMjU6MjA6MTk6MDggKzAwMDBdIDIwMCBcIlBPU1QgL2FwaS92MS9wdXNoIEhUVFAvMS4xXCIgMCBcIi1cIiBcIlByb21ldGhldXMvMi41NC4wXCIgXCItXCJcbiAgICAgICAgICAtIHNldChhdHRyaWJ1dGVzW1wiY2xpZW50X2lwXCJdLCBFeHRyYWN0UGF0dGVybnMoYXR0cmlidXRlc1tcImJvZHlcIl0sIFwiXig/UDxpcD5bMC05Ll0rKVwiKVtcImlwXCJdKSB3aGVyZSBhdHRyaWJ1dGVzW1wiYm9keVwiXSAhPSBuaWwgYW5kIEV4dHJhY3RQYXR0ZXJucyhhdHRyaWJ1dGVzW1wiYm9keVwiXSwgXCJeKD9QPGlwPlswLTkuXSspXCIpICE9IG5pbFxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJyZW1vdGVfdXNlclwiXSwgRXh0cmFjdFBhdHRlcm5zKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIl5bMC05Ll0rIC0gKD9QPHVzZXI+W15cXFxcc10rKVwiKVtcInVzZXJcIl0pIHdoZXJlIGF0dHJpYnV0ZXNbXCJib2R5XCJdICE9IG5pbCBhbmQgRXh0cmFjdFBhdHRlcm5zKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIl5bMC05Ll0rIC0gKD9QPHVzZXI+W15cXFxcc10rKVwiKSAhPSBuaWwgYW5kIG5vdCBJc01hdGNoKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIl5bMC05Ll0rIC0gLVwiKVxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJ0aW1lc3RhbXBcIl0sIEV4dHJhY3RQYXR0ZXJucyhhdHRyaWJ1dGVzW1wiYm9keVwiXSwgXCJcXFxcWyg/UDx0aW1lc3RhbXA+W15cXFxcXV0rKVxcXFxdXCIpW1widGltZXN0YW1wXCJdKSB3aGVyZSBhdHRyaWJ1dGVzW1wiYm9keVwiXSAhPSBuaWwgYW5kIEV4dHJhY3RQYXR0ZXJucyhhdHRyaWJ1dGVzW1wiYm9keVwiXSwgXCJcXFxcWyg/UDx0aW1lc3RhbXA+W15cXFxcXV0rKVxcXFxdXCIpICE9IG5pbFxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJodHRwX3N0YXR1c19jb2RlXCJdLCBJbnQoRXh0cmFjdFBhdHRlcm5zKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIlxcXFxdICg/UDxzdGF0dXM+WzAtOV17M30pXCIpW1wic3RhdHVzXCJdKSkgd2hlcmUgYXR0cmlidXRlc1tcImJvZHlcIl0gIT0gbmlsIGFuZCBFeHRyYWN0UGF0dGVybnMoYXR0cmlidXRlc1tcImJvZHlcIl0sIFwiXFxcXF0gKD9QPHN0YXR1cz5bMC05XXszfSlcIikgIT0gbmlsXG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcImh0dHBfbWV0aG9kXCJdLCBFeHRyYWN0UGF0dGVybnMoYXR0cmlidXRlc1tcImJvZHlcIl0sIFwiXFxcIig/UDxtZXRob2Q+W0EtWl0rKVwiKVtcIm1ldGhvZFwiXSkgd2hlcmUgYXR0cmlidXRlc1tcImJvZHlcIl0gIT0gbmlsIGFuZCBFeHRyYWN0UGF0dGVybnMoYXR0cmlidXRlc1tcImJvZHlcIl0sIFwiXFxcIig/UDxtZXRob2Q+W0EtWl0rKVwiKSAhPSBuaWxcbiAgICAgICAgICAtIHNldChhdHRyaWJ1dGVzW1wiaHR0cF9wYXRoXCJdLCBFeHRyYWN0UGF0dGVybnMoYXR0cmlidXRlc1tcImJvZHlcIl0sIFwiXFxcIltBLVpdKyAoP1A8cGF0aD5bXlxcXFxzXFxcIl0rKVwiKVtcInBhdGhcIl0pIHdoZXJlIGF0dHJpYnV0ZXNbXCJib2R5XCJdICE9IG5pbCBhbmQgRXh0cmFjdFBhdHRlcm5zKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIlxcXCJbQS1aXSsgKD9QPHBhdGg+W15cXFxcc1xcXCJdKylcIikgIT0gbmlsXG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcImh0dHBfcHJvdG9jb2xcIl0sIEV4dHJhY3RQYXR0ZXJucyhhdHRyaWJ1dGVzW1wiYm9keVwiXSwgXCJcXFwiW0EtWl0rIFteXFxcXHNcXFwiXSsgKD9QPHByb3RvY29sPlteXFxcIl0rKVxcXCJcIilbXCJwcm90b2NvbFwiXSkgd2hlcmUgYXR0cmlidXRlc1tcImJvZHlcIl0gIT0gbmlsIGFuZCBFeHRyYWN0UGF0dGVybnMoYXR0cmlidXRlc1tcImJvZHlcIl0sIFwiXFxcIltBLVpdKyBbXlxcXFxzXFxcIl0rICg/UDxwcm90b2NvbD5bXlxcXCJdKylcXFwiXCIpICE9IG5pbFxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJyZXNwb25zZV9zaXplXCJdLCBJbnQoRXh0cmFjdFBhdHRlcm5zKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIlxcXCIgKD9QPHNpemU+WzAtOV0rKSBcXFwiXCIpW1wic2l6ZVwiXSkpIHdoZXJlIGF0dHJpYnV0ZXNbXCJib2R5XCJdICE9IG5pbCBhbmQgRXh0cmFjdFBhdHRlcm5zKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIlxcXCIgKD9QPHNpemU+WzAtOV0rKSBcXFwiXCIpICE9IG5pbFxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJodHRwX3JlZmVyZXJcIl0sIEV4dHJhY3RQYXR0ZXJucyhhdHRyaWJ1dGVzW1wiYm9keVwiXSwgXCJcXFwiIFxcXCIoP1A8cmVmZXJlcj5bXlxcXCJdKylcXFwiIFxcXCJbXlxcXCJdKlxcXCJcIilbXCJyZWZlcmVyXCJdKSB3aGVyZSBhdHRyaWJ1dGVzW1wiYm9keVwiXSAhPSBuaWwgYW5kIEV4dHJhY3RQYXR0ZXJucyhhdHRyaWJ1dGVzW1wiYm9keVwiXSwgXCJcXFwiIFxcXCIoP1A8cmVmZXJlcj5bXlxcXCJdKylcXFwiIFxcXCJbXlxcXCJdKlxcXCJcIikgIT0gbmlsIGFuZCBub3QgSXNNYXRjaChhdHRyaWJ1dGVzW1wiYm9keVwiXSwgXCJcXFwiIFxcXCItXFxcIiBcXFwiXCIpXG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcImh0dHBfdXNlcl9hZ2VudFwiXSwgRXh0cmFjdFBhdHRlcm5zKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIlxcXCIgXFxcIlteXFxcIl0qXFxcIiBcXFwiKD9QPGFnZW50PlteXFxcIl0rKVxcXCJcIilbXCJhZ2VudFwiXSkgd2hlcmUgYXR0cmlidXRlc1tcImJvZHlcIl0gIT0gbmlsIGFuZCBFeHRyYWN0UGF0dGVybnMoYXR0cmlidXRlc1tcImJvZHlcIl0sIFwiXFxcIiBcXFwiW15cXFwiXSpcXFwiIFxcXCIoP1A8YWdlbnQ+W15cXFwiXSspXFxcIlwiKSAhPSBuaWwgYW5kIG5vdCBJc01hdGNoKGF0dHJpYnV0ZXNbXCJib2R5XCJdLCBcIlxcXCIgXFxcIi1cXFwiJFwiKVxuICAgICAgICAgIFxuICAgICAgICAgICMgQWRkIGRlcml2ZWQgYXR0cmlidXRlcyBmb3IgZWFzaWVyIGZpbHRlcmluZ1xuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJpc19zdWNjZXNzXCJdLCB0cnVlKSB3aGVyZSBhdHRyaWJ1dGVzW1wiaHR0cF9zdGF0dXNfY29kZVwiXSA+PSAyMDAgYW5kIGF0dHJpYnV0ZXNbXCJodHRwX3N0YXR1c19jb2RlXCJdIDwgMzAwXG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcImlzX3N1Y2Nlc3NcIl0sIGZhbHNlKSB3aGVyZSBhdHRyaWJ1dGVzW1wiaHR0cF9zdGF0dXNfY29kZVwiXSA8IDIwMCBvciBhdHRyaWJ1dGVzW1wiaHR0cF9zdGF0dXNfY29kZVwiXSA+PSAzMDBcbiAgICAgICAgICAtIHNldChhdHRyaWJ1dGVzW1wiaXNfZXJyb3JcIl0sIHRydWUpIHdoZXJlIGF0dHJpYnV0ZXNbXCJodHRwX3N0YXR1c19jb2RlXCJdID49IDQwMFxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJpc19lcnJvclwiXSwgZmFsc2UpIHdoZXJlIGF0dHJpYnV0ZXNbXCJodHRwX3N0YXR1c19jb2RlXCJdIDwgNDAwXG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcInN0YXR1c19jbGFzc1wiXSwgXCIyeHhcIikgd2hlcmUgYXR0cmlidXRlc1tcImh0dHBfc3RhdHVzX2NvZGVcIl0gPj0gMjAwIGFuZCBhdHRyaWJ1dGVzW1wiaHR0cF9zdGF0dXNfY29kZVwiXSA8IDMwMFxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJzdGF0dXNfY2xhc3NcIl0sIFwiM3h4XCIpIHdoZXJlIGF0dHJpYnV0ZXNbXCJodHRwX3N0YXR1c19jb2RlXCJdID49IDMwMCBhbmQgYXR0cmlidXRlc1tcImh0dHBfc3RhdHVzX2NvZGVcIl0gPCA0MDBcbiAgICAgICAgICAtIHNldChhdHRyaWJ1dGVzW1wic3RhdHVzX2NsYXNzXCJdLCBcIjR4eFwiKSB3aGVyZSBhdHRyaWJ1dGVzW1wiaHR0cF9zdGF0dXNfY29kZVwiXSA+PSA0MDAgYW5kIGF0dHJpYnV0ZXNbXCJodHRwX3N0YXR1c19jb2RlXCJdIDwgNTAwXG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcInN0YXR1c19jbGFzc1wiXSwgXCI1eHhcIikgd2hlcmUgYXR0cmlidXRlc1tcImh0dHBfc3RhdHVzX2NvZGVcIl0gPj0gNTAwIGFuZCBhdHRyaWJ1dGVzW1wiaHR0cF9zdGF0dXNfY29kZVwiXSA8IDYwMFxuICAgICAgICAgICJ9) for Apache/Nginx example. and [ottl.run](https://ottl.run/#eyJ2ZXJzaW9uIjoidjAuMTI4LjAiLCJldmFsdWF0b3IiOiJ0cmFuc2Zvcm1fcHJvY2Vzc29yIiwicGF5bG9hZCI6IntcInJlc291cmNlTG9nc1wiOlt7XCJyZXNvdXJjZVwiOntcImF0dHJpYnV0ZXNcIjpbe1wia2V5XCI6XCJzZXJ2aWNlLm5hbWVcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcInN5c3RlbWQtam91cm5hbFwifX1dfSxcInNjb3BlTG9nc1wiOlt7XCJsb2dSZWNvcmRzXCI6W3tcInRpbWVVbml4TmFub1wiOlwiMTcxOTE3MzI0MDAwMDAwMDAwMFwiLFwiYm9keVwiOntcInN0cmluZ1ZhbHVlXCI6XCJ7XFxcIl9CT09UX0lEXFxcIjpcXFwiYzRhN2I2YjJlOWY0NDI5ZGIxYTVhMWIyYzNkNGU1ZjZcXFwiLFxcXCJfTUFDSElORV9JRFxcXCI6XFxcIjEyMzQ1Njc4OTAxMjM0NTY3ODkwMTIzNDU2Nzg5MDEyXFxcIixcXFwiX0hPU1ROQU1FXFxcIjpcXFwid2ViLXNlcnZlci0wMVxcXCIsXFxcIlBSSU9SSVRZXFxcIjpcXFwiNlxcXCIsXFxcIl9VSURcXFwiOlxcXCIxMDAwXFxcIixcXFwiX0dJRFxcXCI6XFxcIjEwMDBcXFwiLFxcXCJfQ09NTVxcXCI6XFxcIm5naW54XFxcIixcXFwiX0VYRVxcXCI6IFxcXCIvdXNyL3NiaW4vbmdpbnhcXFwiLFxcXCJfQ01ETElORVxcXCI6XFxcIm5naW54OiBtYXN0ZXIgcHJvY2VzcyAvdXNyL3NiaW4vbmdpbnhcXFwiLFxcXCJfQ0FQX0VGRkVDVElWRVxcXCI6XFxcIjBcXFwiLFxcXCJfU1lTVEVNRF9DR1JPVVBcXFwiOlxcXCIvc3lzdGVtLnNsaWNlL25naW54LnNlcnZpY2VcXFwiLFxcXCJfU1lTVEVNRF9VTklUXFxcIjpcXFwibmdpbnguc2VydmljZVxcXCIsXFxcIl9TWVNURU1EX1NMSUNFXFxcIjpcXFwic3lzdGVtLnNsaWNlXFxcIixcXFwiTUVTU0FHRVxcXCI6XFxcIlN0YXJ0ZWQgbmdpbnggLSBoaWdoIHBlcmZvcm1hbmNlIHdlYiBzZXJ2ZXJcXFwiLFxcXCJfUElEXFxcIjpcXFwiMTIzNFxcXCIsXFxcIl9TT1VSQ0VfUkVBTFRJTUVfVElNRVNUQU1QXFxcIjpcXFwiMTcxOTE3MzI0MDEyMzQ1NlxcXCJ9XFxuY2x1c3Rlcjpwcm9kLWNsdXN0ZXJcXG5mbGFnczowXFxuam9iOnN5c3RlbWQtam91cm5hbFxcbm1ldGEuc2lnbmFsX3R5cGU6bG9nXFxubm9kZV9uYW1lOndlYi1zZXJ2ZXItMDFcXG5TYW1wbGUgUmF0ZToxXFxuc2V2ZXJpdHk6aW5mb1xcbnNldmVyaXR5X2NvZGU6NlxcbnRyYW5zcG9ydDpqb3VybmFsXFxuLS0tXCJ9LFwiYXR0cmlidXRlc1wiOlt7XCJrZXlcIjpcImJvZHlcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcIntcXFwiX0JPT1RfSURcXFwiOlxcXCJjNGE3YjZiMmU5ZjQ0MjlkYjFhNWExYjJjM2Q0ZTVmNlxcXCIsXFxcIl9NQUNISU5FX0lEXFxcIjpcXFwiMTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTJcXFwiLFxcXCJfSE9TVE5BTUVcXFwiOlxcXCJ3ZWItc2VydmVyLTAxXFxcIixcXFwiUFJJT1JJVFlcXFwiOlxcXCI2XFxcIixcXFwiX1VJRFxcXCI6XFxcIjEwMDBcXFwiLFxcXCJfR0lEXFxcIjpcXFwiMTAwMFxcXCIsXFxcIl9DT01NXFxcIjpcXFwibmdpbnhcXFwiLFxcXCJfRVhFXFxcIjogXFxcIi91c3Ivc2Jpbi9uZ2lueFxcXCIsXFxcIl9DTURMSU5FXFxcIjpcXFwibmdpbng6IG1hc3RlciBwcm9jZXNzIC91c3Ivc2Jpbi9uZ2lueFxcXCIsXFxcIl9DQVBfRUZGRUNUSVZFXFxcIjpcXFwiMFxcXCIsXFxcIl9TWVNURU1EX0NHUk9VUFxcXCI6XFxcIi9zeXN0ZW0uc2xpY2Uvbmdpbnguc2VydmljZVxcXCIsXFxcIl9TWVNURU1EX1VOSVRcXFwiOlxcXCJuZ2lueC5zZXJ2aWNlXFxcIixcXFwiX1NZU1RFTURfU0xJQ0VcXFwiOlxcXCJzeXN0ZW0uc2xpY2VcXFwiLFxcXCJNRVNTQUdFXFxcIjpcXFwiU3RhcnRlZCBuZ2lueCAtIGhpZ2ggcGVyZm9ybWFuY2Ugd2ViIHNlcnZlclxcXCIsXFxcIl9QSURcXFwiOlxcXCIxMjM0XFxcIixcXFwiX1NPVVJDRV9SRUFMVElNRV9USU1FU1RBTVBcXFwiOlxcXCIxNzE5MTczMjQwMTIzNDU2XFxcIn1cIn19XX0se1widGltZVVuaXhOYW5vXCI6XCIxNzE5MTczMjQxMDAwMDAwMDAwXCIsXCJib2R5XCI6e1wic3RyaW5nVmFsdWVcIjpcIntcXFwiX0JPT1RfSURcXFwiOlxcXCJjNGE3YjZiMmU5ZjQ0MjlkYjFhNWExYjJjM2Q0ZTVmNlxcXCIsXFxcIl9NQUNISU5FX0lEXFxcIjpcXFwiMTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTJcXFwiLFxcXCJfSE9TVE5BTUVcXFwiOlxcXCJ3ZWItc2VydmVyLTAxXFxcIixcXFwiUFJJT1JJVFlcXFwiOlxcXCI0XFxcIixcXFwiX1VJRFxcXCI6XFxcIjBcXFwiLFxcXCJfR0lEXFxcIjpcXFwiMFxcXCIsXFxcIl9DT01NXFxcIjpcXFwic3lzdGVtZFxcXCIsXFxcIl9FWEVcXFwiOlxcXCIvbGliL3N5c3RlbWQvc3lzdGVtZFxcXCIsXFxcIl9DTURMSU5FXFxcIjpcXFwiL2xpYi9zeXN0ZW1kL3N5c3RlbWQgLS1zeXN0ZW0gLS1kZXNlcmlhbGl6ZSAxN1xcXCIsXFxcIl9DQVBfRUZGRUNUSVZFXFxcIjpcXFwiM2ZmZmZmZmZmZlxcXCIsXFxcIl9TWVNURU1EX0NHUk9VUFxcXCI6XFxcIi9pbml0LnNjb3BlXFxcIixcXFwiTUVTU0FHRVxcXCI6XFxcIkZhaWxlZCB0byBzdGFydCBwb3N0Z3Jlc3FsLnNlcnZpY2UgLSBQb3N0Z3JlU1FMIGRhdGFiYXNlIHNlcnZlclxcXCIsXFxcIl9QSURcXFwiOlxcXCIxXFxcIixcXFwiVU5JVFxcXCI6XFxcInBvc3RncmVzcWwuc2VydmljZVxcXCIsXFxcIl9TT1VSQ0VfUkVBTFRJTUVfVElNRVNUQU1QXFxcIjpcXFwiMTcxOTE3MzI0MTQ1Njc4OVxcXCJ9XFxuY2x1c3Rlcjpwcm9kLWNsdXN0ZXJcXG5mbGFnczowXFxuam9iOnN5c3RlbWQtam91cm5hbFxcbm1ldGEuc2lnbmFsX3R5cGU6bG9nXFxubm9kZV9uYW1lOndlYi1zZXJ2ZXItMDFcXG5TYW1wbGUgUmF0ZToxXFxuc2V2ZXJpdHk6d2FyblxcbnNldmVyaXR5X2NvZGU6NFxcbnRyYW5zcG9ydDpqb3VybmFsXFxuLS0tXCJ9LFwiYXR0cmlidXRlc1wiOlt7XCJrZXlcIjpcImJvZHlcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcIntcXFwiX0JPT1RfSURcXFwiOlxcXCJjNGE3YjZiMmU5ZjQ0MjlkYjFhNWExYjJjM2Q0ZTVmNlxcXCIsXFxcIl9NQUNISU5FX0lEXFxcIjpcXFwiMTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTJcXFwiLFxcXCJfSE9TVE5BTUVcXFwiOlxcXCJ3ZWItc2VydmVyLTAxXFxcIixcXFwiUFJJT1JJVFlcXFwiOlxcXCI0XFxcIixcXFwiX1VJRFxcXCI6XFxcIjBcXFwiLFxcXCJfR0lEXFxcIjpcXFwiMFxcXCIsXFxcIl9DT01NXFxcIjpcXFwic3lzdGVtZFxcXCIsXFxcIl9FWEVcXFwiOlxcXCIvbGliL3N5c3RlbWQvc3lzdGVtZFxcXCIsXFxcIl9DTURMSU5FXFxcIjpcXFwiL2xpYi9zeXN0ZW1kL3N5c3RlbWQgLS1zeXN0ZW0gLS1kZXNlcmlhbGl6ZSAxN1xcXCIsXFxcIl9DQVBfRUZGRUNUSVZFXFxcIjpcXFwiM2ZmZmZmZmZmZlxcXCIsXFxcIl9TWVNURU1EX0NHUk9VUFxcXCI6XFxcIi9pbml0LnNjb3BlXFxcIixcXFwiTUVTU0FHRVxcXCI6XFxcIkZhaWxlZCB0byBzdGFydCBwb3N0Z3Jlc3FsLnNlcnZpY2UgLSBQb3N0Z3JlU1FMIGRhdGFiYXNlIHNlcnZlclxcXCIsXFxcIl9QSURcXFwiOlxcXCIxXFxcIixcXFwiVU5JVFxcXCI6XFxcInBvc3RncmVzcWwuc2VydmljZVxcXCIsXFxcIl9TT1VSQ0VfUkVBTFRJTUVfVElNRVNUQU1QXFxcIjpcXFwiMTcxOTE3MzI0MTQ1Njc4OVxcXCJ9XCJ9fV19LHtcInRpbWVVbml4TmFub1wiOlwiMTcxOTE3MzI0MjAwMDAwMDAwMFwiLFwiYm9keVwiOntcInN0cmluZ1ZhbHVlXCI6XCJ7XFxcIl9CT09UX0lEXFxcIjpcXFwiYzRhN2I2YjJlOWY0NDI5ZGIxYTVhMWIyYzNkNGU1ZjZcXFwiLFxcXCJfTUFDSElORV9JRFxcXCI6XFxcIjEyMzQ1Njc4OTAxMjM0NTY3ODkwMTIzNDU2Nzg5MDEyXFxcIixcXFwiX0hPU1ROQU1FXFxcIjpcXFwid2ViLXNlcnZlci0wMVxcXCIsXFxcIlBSSU9SSVRZXFxcIjpcXFwiM1xcXCIsXFxcIl9VSURcXFwiOlxcXCI5OTdcXFwiLFxcXCJfR0lEXFxcIjpcXFwiOTk3XFxcIixcXFwiX0NPTU1cXFwiOlxcXCJyZWRpcy1zZXJ2ZXJcXFwiLFxcXCJfRVhFXFxcIjpcXFwiL3Vzci9iaW4vcmVkaXMtc2VydmVyXFxcIixcXFwiX0NNRExJTkVcXFwiOlxcXCJyZWRpcy1zZXJ2ZXIgKjo2Mzc5XFxcIixcXFwiX0NBUF9FRkZFQ1RJVkVcXFwiOlxcXCIwXFxcIixcXFwiX1NZU1RFTURfQ0dST1VQXFxcIjpcXFwiL3N5c3RlbS5zbGljZS9yZWRpcy5zZXJ2aWNlXFxcIixcXFwiX1NZU1RFTURfVU5JVFxcXCI6XFxcInJlZGlzLnNlcnZpY2VcXFwiLFxcXCJfU1lTVEVNRF9TTElDRVxcXCI6XFxcInN5c3RlbS5zbGljZVxcXCIsXFxcIk1FU1NBR0VcXFwiOlxcXCJDb25uZWN0aW9uIHJlZnVzZWQgYnkgc2VydmVyIGF0IDEyNy4wLjAuMTo2Mzc5XFxcIixcXFwiX1BJRFxcXCI6XFxcIjU2NzhcXFwiLFxcXCJTWVNMT0dfSURFTlRJRklFUlxcXCI6XFxcInJlZGlzLXNlcnZlclxcXCIsXFxcIl9TT1VSQ0VfUkVBTFRJTUVfVElNRVNUQU1QXFxcIjpcXFwiMTcxOTE3MzI0Mjc4OTAxMlxcXCJ9XFxuY2x1c3Rlcjpwcm9kLWNsdXN0ZXJcXG5mbGFnczowXFxuam9iOnN5c3RlbWQtam91cm5hbFxcbm1ldGEuc2lnbmFsX3R5cGU6bG9nXFxubm9kZV9uYW1lOndlYi1zZXJ2ZXItMDFcXG5TYW1wbGUgUmF0ZToxXFxuc2V2ZXJpdHk6ZXJyb3JcXG5zZXZlcml0eV9jb2RlOjNcXG50cmFuc3BvcnQ6am91cm5hbFxcbi0tLVwifSxcImF0dHJpYnV0ZXNcIjpbe1wia2V5XCI6XCJib2R5XCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJ7XFxcIl9CT09UX0lEXFxcIjpcXFwiYzRhN2I2YjJlOWY0NDI5ZGIxYTVhMWIyYzNkNGU1ZjZcXFwiLFxcXCJfTUFDSElORV9JRFxcXCI6XFxcIjEyMzQ1Njc4OTAxMjM0NTY3ODkwMTIzNDU2Nzg5MDEyXFxcIixcXFwiX0hPU1ROQU1FXFxcIjpcXFwid2ViLXNlcnZlci0wMVxcXCIsXFxcIlBSSU9SSVRZXFxcIjpcXFwiM1xcXCIsXFxcIl9VSURcXFwiOlxcXCI5OTdcXFwiLFxcXCJfR0lEXFxcIjpcXFwiOTk3XFxcIixcXFwiX0NPTU1cXFwiOlxcXCJyZWRpcy1zZXJ2ZXJcXFwiLFxcXCJfRVhFXFxcIjpcXFwiL3Vzci9iaW4vcmVkaXMtc2VydmVyXFxcIixcXFwiX0NNRExJTkVcXFwiOlxcXCJyZWRpcy1zZXJ2ZXIgKjo2Mzc5XFxcIixcXFwiX0NBUF9FRkZFQ1RJVkVcXFwiOlxcXCIwXFxcIixcXFwiX1NZU1RFTURfQ0dST1VQXFxcIjpcXFwiL3N5c3RlbS5zbGljZS9yZWRpcy5zZXJ2aWNlXFxcIixcXFwiX1NZU1RFTURfVU5JVFxcXCI6XFxcInJlZGlzLnNlcnZpY2VcXFwiLFxcXCJfU1lTVEVNRF9TTElDRVxcXCI6XFxcInN5c3RlbS5zbGljZVxcXCIsXFxcIk1FU1NBR0VcXFwiOlxcXCJDb25uZWN0aW9uIHJlZnVzZWQgYnkgc2VydmVyIGF0IDEyNy4wLjAuMTo2Mzc5XFxcIixcXFwiX1BJRFxcXCI6XFxcIjU2NzhcXFwiLFxcXCJTWVNMT0dfSURFTlRJRklFUlxcXCI6XFxcInJlZGlzLXNlcnZlclxcXCIsXFxcIl9TT1VSQ0VfUkVBTFRJTUVfVElNRVNUQU1QXFxcIjpcXFwiMTcxOTE3MzI0Mjc4OTAxMlxcXCJ9XCJ9fV19LHtcInRpbWVVbml4TmFub1wiOlwiMTcxOTE3MzI0MzAwMDAwMDAwMFwiLFwiYm9keVwiOntcInN0cmluZ1ZhbHVlXCI6XCJ7XFxcImVycm5vXFxcIjpcXFwiNlxcXCIsXFxcInByaW9yaXR5XFxcIjpcXFwiaW5mb1xcXCIsXFxcInVuaXRcXFwiOlxcXCJjb250YWluZXJkLnNlcnZpY2VcXFwiLFxcXCJfZW50cnlcXFwiOlxcXCJ0aW1lPVxcXFxcXFwiMjAyNS0wNi0yNFQwMjo0MDo0NC4yODkzODczOTdaXFxcXFxcXCIgbGV2ZWw9ZXJyb3IgbXNnPVxcXFxcXFwiRmFpbGVkIHRvIGdldCB1c2FnZSBmb3Igc25hcHNob3QgXFxcXFxcXFxcXFxcXFxcIjY0ODdiODBhYzNlZmNkNmRlNmQ1ODA1MWVkNDA2ZmI1MDEzZGNjMzhkNmJjZWU2OGNmMTFkMzFiM2E1NGMyZThcXFxcXFxcXFxcXFxcXFwiXFxcXFxcXCIgZXJyb3I9XFxcXFxcXCJsc3RhdCAvdmFyL2xpYi9jb250YWluZXJkL2lvLmNvbnRhaW5lcmQuc25hcHNob3R0ZXIudjEub3ZlcmxheWZzL3NuYXBzaG90cy82MS9mcy9ldGMvc2VydmljZS9lbmFibGVkL21vbml0b3ItYWRkcmVzc2VzL3N1cGVydmlzZS9zdGF0dXMubmV3OiBubyBzdWNoIGZpbGUgb3IgZGlyZWN0b3J5XFxcXFxcXCJcXFwifVxcbmNsdXN0ZXI6c294Mi11c2UyXFxuZmxhZ3M6MFxcbmpvYjpzeXN0ZW1kLWpvdXJuYWxcXG5tZXRhLnNpZ25hbF90eXBlOmxvZ1xcbm5vZGVfbmFtZTppcC0xNzItMTYtNzctMTk1LnVzLWVhc3QtMi5jb21wdXRlLmludGVybmFsXFxuU2FtcGxlIFJhdGU6MVxcbnNldmVyaXR5OnVuc3BlY2lmaWVkXFxuc2V2ZXJpdHlfY29kZTowXFxudHJhbnNwb3J0OnN0ZG91dFxcbi0tLVwifSxcImF0dHJpYnV0ZXNcIjpbe1wia2V5XCI6XCJib2R5XCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJ7XFxcImVycm5vXFxcIjpcXFwiNlxcXCIsXFxcInByaW9yaXR5XFxcIjpcXFwiaW5mb1xcXCIsXFxcInVuaXRcXFwiOlxcXCJjb250YWluZXJkLnNlcnZpY2VcXFwiLFxcXCJfZW50cnlcXFwiOlxcXCJ0aW1lPVxcXFxcXFwiMjAyNS0wNi0yNFQwMjo0MDo0NC4yODkzODczOTdaXFxcXFxcXCIgbGV2ZWw9ZXJyb3IgbXNnPVxcXFxcXFwiRmFpbGVkIHRvIGdldCB1c2FnZSBmb3Igc25hcHNob3QgXFxcXFxcXFxcXFxcXFxcIjY0ODdiODBhYzNlZmNkNmRlNmQ1ODA1MWVkNDA2ZmI1MDEzZGNjMzhkNmJjZWU2OGNmMTFkMzFiM2E1NGMyZThcXFxcXFxcXFxcXFxcXFwiXFxcXFxcXCIgZXJyb3I9XFxcXFxcXCJsc3RhdCAvdmFyL2xpYi9jb250YWluZXJkL2lvLmNvbnRhaW5lcmQuc25hcHNob3R0ZXIudjEub3ZlcmxheWZzL3NuYXBzaG90cy82MS9mcy9ldGMvc2VydmljZS9lbmFibGVkL21vbml0b3ItYWRkcmVzc2VzL3N1cGVydmlzZS9zdGF0dXMubmV3OiBubyBzdWNoIGZpbGUgb3IgZGlyZWN0b3J5XFxcXFxcXCJcXFwifVwifX0se1wia2V5XCI6XCJ0cmFuc3BvcnRcIixcInZhbHVlXCI6e1wic3RyaW5nVmFsdWVcIjpcInN0ZG91dFwifX0se1wia2V5XCI6XCJjbHVzdGVyXCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJzb3gyLXVzZTJcIn19LHtcImtleVwiOlwiZmxhZ3NcIixcInZhbHVlXCI6e1wiaW50VmFsdWVcIjpcIjBcIn19LHtcImtleVwiOlwiam9iXCIsXCJ2YWx1ZVwiOntcInN0cmluZ1ZhbHVlXCI6XCJzeXN0ZW1kLWpvdXJuYWxcIn19LHtcImtleVwiOlwibWV0YS5zaWduYWxfdHlwZVwiLFwidmFsdWVcIjp7XCJzdHJpbmdWYWx1ZVwiOlwibG9nXCJ9fSx7XCJrZXlcIjpcIm5vZGVfbmFtZVwiLFwidmFsdWVcIjp7XCJzdHJpbmdWYWx1ZVwiOlwiaXAtMTcyLTE2LTc3LTE5NS51cy1lYXN0LTIuY29tcHV0ZS5pbnRlcm5hbFwifX0se1wia2V5XCI6XCJTYW1wbGUgUmF0ZVwiLFwidmFsdWVcIjp7XCJpbnRWYWx1ZVwiOlwiMVwifX0se1wia2V5XCI6XCJzZXZlcml0eVwiLFwidmFsdWVcIjp7XCJzdHJpbmdWYWx1ZVwiOlwidW5zcGVjaWZpZWRcIn19LHtcImtleVwiOlwic2V2ZXJpdHlfY29kZVwiLFwidmFsdWVcIjp7XCJpbnRWYWx1ZVwiOlwiMFwifX1dfV19XX1dfSIsImNvbmZpZyI6ImVycm9yX21vZGU6IGlnbm9yZVxubG9nX3N0YXRlbWVudHM6XG4gICAgLSBjb250ZXh0OiBsb2dcbiAgICAgIHN0YXRlbWVudHM6XG4gICAgICAgICAgIyBQYXJzZSBIVFRQIGFjY2VzcyBsb2cgZnJvbSBib2R5IGF0dHJpYnV0ZSAoYWxyZWFkeSBleHRyYWN0ZWQgZnJvbSBib2R5OiBrZXktdmFsdWUgcGFpcilcbiAgICAgICAgICAjIEV4YW1wbGUgYm9keSBhdHRyaWJ1dGU6IDE3Mi4xNi43NC45MyAtIC0gWzIzL0p1bi8yMDI1OjIwOjE5OjA4ICswMDAwXSAyMDAgXCJQT1NUIC9hcGkvdjEvcHVzaCBIVFRQLzEuMVwiIDAgXCItXCIgXCJQcm9tZXRoZXVzLzIuNTQuMFwiIFwiLVwiXG5cbiAgICAgICAgICAgIyBQYXJzZSBzeXN0ZW1kIGxvZ3MgZGlyZWN0bHkgZnJvbSBib2R5XG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcImVycm5vXCJdLCBFeHRyYWN0UGF0dGVybnMoYm9keSwgXCJcXFwiZXJybm9cXFwiOlxcXCIoP1A8ZXJybm8+W15cXFwiXSspXFxcIlwiKVtcImVycm5vXCJdKSB3aGVyZSBFeHRyYWN0UGF0dGVybnMoYm9keSwgXCJcXFwiZXJybm9cXFwiOlxcXCIoP1A8ZXJybm8+W15cXFwiXSspXFxcIlwiKSAhPSBuaWxcbiAgICAgICAgICAtIHNldChhdHRyaWJ1dGVzW1wibG9nX3ByaW9yaXR5XCJdLCBFeHRyYWN0UGF0dGVybnMoYm9keSwgXCJcXFwicHJpb3JpdHlcXFwiOlxcXCIoP1A8cHJpb3JpdHk+W15cXFwiXSspXFxcIlwiKVtcInByaW9yaXR5XCJdKSB3aGVyZSBFeHRyYWN0UGF0dGVybnMoYm9keSwgXCJcXFwicHJpb3JpdHlcXFwiOlxcXCIoP1A8cHJpb3JpdHk+W15cXFwiXSspXFxcIlwiKSAhPSBuaWxcbiAgICAgICAgICAtIHNldChhdHRyaWJ1dGVzW1wibG9nX2VudHJ5XCJdLCBFeHRyYWN0UGF0dGVybnMoYm9keSwgXCJcXFwiX2VudHJ5XFxcIjpcXFwiKD9QPGVudHJ5Pi4qPylcXFwiXFxcXH1cIilbXCJlbnRyeVwiXSkgd2hlcmUgRXh0cmFjdFBhdHRlcm5zKGJvZHksIFwiXFxcIl9lbnRyeVxcXCI6XFxcIig/UDxlbnRyeT4uKj8pXFxcIlxcXFx9XCIpICE9IG5pbFxuICAgICAgICAgIC0gc2V0KGF0dHJpYnV0ZXNbXCJzeXN0ZW1kX3VuaXRcIl0sIEV4dHJhY3RQYXR0ZXJucyhib2R5LCBcIlxcXCJ1bml0XFxcIjpcXFwiKD9QPHVuaXQ+W15cXFwiXSspXFxcIlwiKVtcInVuaXRcIl0pIHdoZXJlIEV4dHJhY3RQYXR0ZXJucyhib2R5LCBcIlxcXCJ1bml0XFxcIjpcXFwiKD9QPHVuaXQ+W15cXFwiXSspXFxcIlwiKSAhPSBuaWxcbiAgICAgICAgICBcbiAgICAgICAgICAjIEV4dHJhY3QgY29udGFpbmVyZCBsb2cgbGV2ZWwgZnJvbSBfZW50cnkgZmllbGRcbiAgICAgICAgICAtIHNldChhdHRyaWJ1dGVzW1wiY29udGFpbmVyZF9sZXZlbFwiXSwgRXh0cmFjdFBhdHRlcm5zKGJvZHksIFwibGV2ZWw9KD9QPGxldmVsPlthLXpdKylcIilbXCJsZXZlbFwiXSkgd2hlcmUgRXh0cmFjdFBhdHRlcm5zKGJvZHksIFwibGV2ZWw9KD9QPGxldmVsPlthLXpdKylcIikgIT0gbmlsXG4gICAgICAgICAgLSBzZXQoYXR0cmlidXRlc1tcImNvbnRhaW5lcmRfbXNnXCJdLCBFeHRyYWN0UGF0dGVybnMoYm9keSwgXCJtc2c9XFxcXFxcXFxcXFxcXFxcIig/UDxtc2c+Lio/KVxcXFxcXFxcXFxcXFxcXCIgZXJyb3I9XCIpW1wibXNnXCJdKSB3aGVyZSBFeHRyYWN0UGF0dGVybnMoYm9keSwgXCJtc2c9XFxcXFxcXFxcXFxcXFxcIig/UDxtc2c+Lio/KVxcXFxcXFxcXFxcXFxcXCIgZXJyb3I9XCIpICE9IG5pbFxuIn0=) for systemd/journald example

### Extract HTTP Access Log Fields

These examples parse Apache/Nginx combined log format from the `body` attribute:

```javascript
// Extract client IP address (e.g., "172.16.74.93" from start of log line)
// Creates attribute["client_ip"] = "172.16.74.93"
set(
  attributes['client_ip'],
  ExtractPatterns(attributes['body'], '^(?P<ip>[0-9.]+)')['ip']
)

// Extract HTTP status code as integer (e.g., 200 from "] 200 \"")
// Creates attribute["http_status_code"] = 200 (integer)
set(
  attributes['http_status_code'],
  Int(ExtractPatterns(attributes['body'], '\\] (?P<status>[0-9]{3})')['status'])
)

// Extract HTTP method (e.g., "POST" from "\"POST /api/v1/push")
// Creates attribute["http_method"] = "POST"
set(
  attributes['http_method'],
  ExtractPatterns(attributes['body'], '"(?P<method>[A-Z]+)')['method']
)

// Extract request path (e.g., "/api/v1/push" from "POST /api/v1/push HTTP/1.1")
// Creates attribute["http_path"] = "/api/v1/push"
set(
  attributes['http_path'],
  ExtractPatterns(attributes['body'], '"[A-Z]+ (?P<path>[^\\s"]+)')['path']
)

// Extract user agent (e.g., "Prometheus/2.54.0" from last quoted field)
// Creates attribute["http_user_agent"] = "Prometheus/2.54.0"
set(
  attributes['http_user_agent'],
  ExtractPatterns(attributes['body'], '" "[^"]*" "(?P<agent>[^"]+)"')['agent']
)
```

### Derived Attributes and Conditions

These examples create useful derived fields and use conditional logic:

```javascript
// Create boolean success flag for 2xx status codes
// Creates attribute["is_success"] = true/false
set(attributes["is_success"], true) where attributes["http_status_code"] >= 200 and attributes["http_status_code"] < 300

// Create status class categorization (e.g., "4xx" for client errors)
// Creates attribute["status_class"] = "2xx", "3xx", "4xx", or "5xx"
set(attributes["status_class"], "4xx") where attributes["http_status_code"] >= 400 and attributes["http_status_code"] < 500

// Only extract remote user if not a dash (authenticated users only)
// Creates attribute["remote_user"] only when user is authenticated
set(attributes["remote_user"], ExtractPatterns(attributes["body"], "^[0-9.]+ - (?P<user>[^\\s]+)")["user"])
  where attributes["body"] != nil and not IsMatch(attributes["body"], "^[0-9.]+ - -")
```

### Run OTEL Collector (optional), only tested in ottl.run currently

Set environment variables:

```bash
export OTEL_EXPORTER_OTLP_ENDPOINT="https://api.honeycomb.io"
export HONEYCOMB_API_KEY="your-api-key"
```

Run the collector:

```bash
otelcol-contrib --config configs/basic-collector.yaml
```

### View Parsed Logs

The collector will:

1. Read logs from configured file sources
2. Parse structured fields using transform processor
3. Export to configured OTLP endpoint (Honeycomb, etc.)
4. Output debug logs showing parsed attributes

## Configuration Details

The `basic-collector.yaml` includes:

- **filelog receiver**: Reads from `/tmp/simple-logs.log`
- **transform processor**: Parses key-value pairs and JSON bodies
- **batch processor**: Batches logs for efficient export
- **resource processor**: Adds service name
- **OTLP exporter**: Sends to Honeycomb or other OTLP endpoints

## Parsed Attributes

### Nginx Logs

- `http_ip`: Client IP address
- `http_method`: HTTP method (GET, POST, etc.)
- `http_path`: Request path
- `http_status`: HTTP status code
- `http_user_agent`: User agent string

### Systemd Logs

- `errno`: System error number
- `log_priority`: Log priority level (info, warn, error, debug)
- `log_entry`: Log message content
- `transport`: Log transport method (journal)

### Common Attributes

- `app`: Application name
- `cluster`: Cluster identifier
- `component`: Component name (nginx, etc.)
- `job`: Job name
- `namespace`: Kubernetes namespace
- `node_name`: Node name
- `pod`: Pod name
- `severity`: Log severity
- `severity_code`: Numeric severity code

## Testing

1. Configure your log sources in the collector configuration

2. Run the OTEL collector:

   ```bash
   otelcol-contrib --config configs/basic-collector.yaml
   ```

3. Check the collector output for parsed attributes and successful exports

4. Use the JSON examples with [ottl.run](https://ottl.run) to test parsing expressions

## Honeycomb Derived Columns and Calculated Fields

If you need additional parsing beyond what the OTEL collector provides, you can use Honeycomb's derived columns and calculated fields to extract data from the `body` field.

### Setting Universal Message Schema Field

To set up a universal message field in Honeycomb, create a derived column named `message` using this formula:

```javascript
// Universal message extractor for all 3 log types
IF(
  CONTAINS($body, '{"errno"'),
  REG_VALUE($body, '"_entry":"([^"]+)"'),
  IF(
    CONTAINS($body, 'HTTP/1.1'),
    CONCAT(
      REG_VALUE($body, '"([A-Z]+)'),
      ':',
      REG_VALUE($body, '[A-Z]+ ([^\\s]+)'),
      ':',
      REG_VALUE($body, '\\] (\\d+) "')
    ),
    IF(
      CONTAINS($body, 'query='),
      REG_VALUE($body, 'query="([^"]+)"'),
      'unknown'
    )
  )
)
```

This creates a unified `message` field that extracts:

- **Systemd logs**: `"Removed slice User Slice of root."`
- **Nginx logs**: `"POST:/api/v1/push:200"`
- **Loki logs**: `"rate({type=\"appserver/appserver-licensing\"} |= \"License currently in use:\" ...)"`
- **Fallback**: `"unknown"` for unrecognized formats

**Setup Steps:**

1. Go to your Honeycomb dataset
2. Navigate to "Schema" → "Derived Columns"
3. Create new derived column named `log.message-univ`. This is the first formula below.
4. Update dataset definitions and change `log.message-univ` to
5. Save and the field will be available for queries and visualizations

### Derived Columns/Calculated Fields Examples

#### Extract Important Messages (Universal) for viewing in UI

```javascript
// Universal message extractor - works for all 3 log types
IF(
  CONTAINS($body, '{"errno"'),
  REG_VALUE($body, '"_entry":"([^"]+)"'),
  IF(
    CONTAINS($body, 'HTTP/1.1'),
    CONCAT(
      REG_VALUE($body, '"([A-Z]+)'),
      ':',
      REG_VALUE($body, '[A-Z]+ ([^\\s]+)'),
      ':'
    ),
    IF(
      CONTAINS($body, 'query='),
      REG_VALUE($body, 'query="([^"]+)"'),
      'unknown'
    )
  )
)
```

#### Extract HTTP Fields from Body

```javascript
// HTTP Status Code
REG_VALUE($body, '\\] (\\d+) "')

// HTTP Method
REG_VALUE($body, '"([A-Z]+)')

// Client IP Address
REG_VALUE($body, '^(\\d+\\.\\d+\\.\\d+\\.\\d+)')

// Request Path
REG_VALUE($body, '[A-Z]+ ([^\\s]+)')

// User Agent
REG_VALUE($body, '"([^"]+)" "-"$')
```

#### Extract JSON Fields from Systemd Logs

````javascript
// Log Priority
REG_VALUE($body, "\"priority\":\"([^\"]+)\"")

// Log Entry Message
REG_VALUE($body, "\"_entry\":\"([^\"]+)\"")


#### Extract Important Messages (Individual Functions)

```javascript
// For Nginx logs: "POST:/api/v1/push:200"
CONCAT(REG_VALUE($body, "\"([A-Z]+)"), ":", REG_VALUE($body, "[A-Z]+ ([^\\s]+)"), ":", REG_VALUE($body, "\\] (\\d+) \""))

// For Systemd logs: "_entry" field
REG_VALUE($body, "\"_entry\":\"([^\"]+)\"")

// For Loki logs: LogQL query
REG_VALUE($body, "query=\"([^\"]+)\"")
````

### Calculated Fields Examples

#### HTTP Status Categorization

```javascript
// Using conditional operators (IF function)
IF(
  STARTS_WITH(REG_VALUE($body, '\\] (\\d+) "'), '2'),
  'Success',
  IF(
    STARTS_WITH(REG_VALUE($body, '\\] (\\d+) "'), '3'),
    'Redirect',
    IF(
      STARTS_WITH(REG_VALUE($body, '\\] (\\d+) "'), '4'),
      'Client Error',
      IF(
        STARTS_WITH(REG_VALUE($body, '\\] (\\d+) "'), '5'),
        'Server Error',
        'Unknown'
      )
    )
  )
)
```

#### Log Type Detection

```javascript
// Using EXISTS and CONTAINS functions
IF(
  CONTAINS($body, '{"errno"'),
  'systemd',
  IF(CONTAINS($body, 'HTTP/1.1'), 'nginx', 'unknown')
)
```

#### Priority Level Mapping

```javascript
// Using nested IF conditions
IF(REG_VALUE($body, "\"priority\":\"([^\"]+)\"") = "debug", 1,
   IF(REG_VALUE($body, "\"priority\":\"([^\"]+)\"") = "info", 2,
      IF(REG_VALUE($body, "\"priority\":\"([^\"]+)\"") = "warn", 3,
         IF(REG_VALUE($body, "\"priority\":\"([^\"]+)\"") = "error", 4, 0))))
```

#### Error Detection (Boolean)

```javascript
// Using OR conditions with STARTS_WITH
STARTS_WITH(REG_VALUE($body, "\\] (\\d+) \""), "4") OR
STARTS_WITH(REG_VALUE($body, "\\] (\\d+) \""), "5") OR
REG_VALUE($body, "\"priority\":\"([^\"]+)\"") = "error"
```

#### API Endpoint Categorization

```javascript
// Using nested IF with STARTS_WITH
IF(
  STARTS_WITH(REG_VALUE($body, '"[A-Z]+ ([^"]+)"'), '/api/v1/'),
  'API v1',
  IF(
    STARTS_WITH(REG_VALUE($body, '"[A-Z]+ ([^"]+)"'), '/api/v2/'),
    'API v2',
    IF(
      STARTS_WITH(REG_VALUE($body, '"[A-Z]+ ([^"]+)"'), '/health'),
      'Health Check',
      IF(
        STARTS_WITH(REG_VALUE($body, '"[A-Z]+ ([^"]+)"'), '/metrics'),
        'Metrics',
        'Other'
      )
    )
  )
)
```

#### Browser Detection from User Agent

```javascript
// Using CONTAINS function with nested IF
IF(
  CONTAINS(REG_VALUE($body, '"([^"]+)" "-"$'), 'Chrome'),
  'Chrome',
  IF(
    CONTAINS(REG_VALUE($body, '"([^"]+)" "-"$'), 'Firefox'),
    'Firefox',
    IF(
      CONTAINS(REG_VALUE($body, '"([^"]+)" "-"$'), 'Safari'),
      'Safari',
      IF(
        CONTAINS(REG_VALUE($body, '"([^"]+)" "-"$'), 'Prometheus'),
        'Prometheus',
        'Other'
      )
    )
  )
)
```

### Usage Tips

1. **Test with REG_MATCH first**: Use `REG_MATCH($body, "pattern")` to verify your regex pattern exists, then use `REG_VALUE($body, "pattern")` to extract the value
2. **Use multiple derived columns**: Break complex parsing into smaller, reusable columns
3. **Add error handling**: Use nested `IF()` statements or `EXISTS()` functions for missing values
4. **Performance**: Derived columns are calculated at query time, so simpler expressions perform better
5. **Debugging**: Start with simple extractions and build complexity gradually
6. **Use proper functions**: Honeycomb uses `IF()`, `CONTAINS()`, `STARTS_WITH()`, and `OR`/`AND` instead of `CASE` statements

### When to Use Derived Columns vs OTEL Parsing

- **Use OTEL parsing** for consistent fields you want indexed and searchable
- **Use derived columns** for ad-hoc analysis, complex transformations, or fields you don't need indexed
- **Combine both** for maximum flexibility - parse common fields in OTEL, use derived columns for specialized analysis
