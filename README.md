# kbro

Minimal WebKit2 kiosk browser for dashboards and persistent displays. Opens a single undecorated maximized window and loads a URL — nothing else.

## Dependencies

System packages only (no pip dependencies):

```
sudo apt install python3-gi python3-gi-cairo gir1.2-gtk-3.0 gir1.2-webkit2-4.1
```

## Usage

```
kbro [options] url
```

If the URL has no scheme, `http://` is assumed.

### Window options

| Flag | Description |
|------|-------------|
| *(default)* | Undecorated, maximized window |
| `--fullscreen` | True fullscreen (hides taskbar) |
| `--no-maximize` | Normal windowed mode |
| `--decorated` | Show title bar and window borders |
| `--refresh N` | Reload page every N seconds |

`--fullscreen` and `--no-maximize` are mutually exclusive.

### Logging options

| Flag | Description |
|------|-------------|
| `--verbose` | Show page load events and extra detail |
| `--debug` | Show debug output; also enables the WebKit inspector |
| `--trace` | Full trace output (implies `--debug`) |
| `--logfile FILE` | Write log output to FILE in addition to stderr |
| `--syslog` | Also send log output to syslog |

`--verbose`, `--debug`, and `--trace` are mutually exclusive.

## Examples

```bash
# Dashboard on a local service
./kbro http://localhost:3000

# Grafana board, fullscreen
./kbro --fullscreen https://grafana.example.com/d/abc123

# Debug a page with the WebKit inspector
./kbro --debug http://localhost:8080

# Auto-refresh every 60 seconds
./kbro --refresh 60 http://dashboard.local

# Log to file
./kbro --verbose --logfile /var/log/kbro.log http://dashboard.local
```
