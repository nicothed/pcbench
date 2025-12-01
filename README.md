# PC Benchmark Tool - Native Windows Application

A comprehensive PC benchmarking tool built with Neutralino.js that provides both browser-based and native Windows performance testing.

Check out the browser version on https://nicothed.github.io/pcbench/pcbench.html

## Features

### Native Windows Features (via Neutralino APIs)
- **Real System Info**: CPU name, cores/threads, actual RAM size, GPU name
- **Drive Detection**: All drives with usage bars (color-coded warnings)
- **System Uptime**: How long since last boot
- **Process Count**: Number of running processes
- **Native Disk I/O**: Real file read/write speed testing
- **Memory Monitoring**: Real-time available RAM tracking

### Benchmark Tests
| Test | Type | What it measures |
|------|------|------------------|
| CPU | Browser | Mathematical computations (prime sieve, matrix multiplication, trig) |
| GPU | Browser | WebGL rendering (10,000 triangles with shaders) |
| RAM | Browser | Memory bandwidth (typed array operations) |
| Display | Browser | Canvas 2D rendering (500 animated particles) |
| Disk I/O | Native | Actual file write/read speeds |
| Health | Hybrid | Timer jitter, frame consistency, process load |
| Memory | Native | Available RAM percentage |
| Network | Browser | Download speed (Cloudflare CDN) - not scored |

### Additional Features
- Test history stored persistently (up to 20 runs)
- Graphical history chart with hover details
- Score breakdown by component
- Rating system (Excellent/Great/Good/Average/Low)

## Build Instructions

### Prerequisites
1. **Node.js** (v14 or higher) - https://nodejs.org/
2. **Neutralino CLI**:
   ```bash
   npm install -g @neutralinojs/neu
   ```

### Build Steps

1. **Navigate to project folder**:
   ```bash
  REM NOT REQUIRED 
   ```

2. **Download Neutralino binaries**:
   ```bash
   neu update
   ```
   This downloads the Neutralino runtime (~5MB) and client library.

3. **Run in development mode** (optional, for testing):
   ```bash
   neu run
   ```

4. **Build release version**:
   ```bash
   neu build --release
   ```

5. **Find your executable**:
   ```
   dist/
   └── PCBenchmark/
       ├── PCBenchmark-win_x64.exe    ← Windows 64-bit executable
       ├── resources.neu              ← App resources (HTML/JS/CSS)
       └── WebView2Loader.dll         ← Required DLL
   ```

### Distribution

To distribute your app, zip the entire `dist/PCBenchmark/` folder. Users need:
- `PCBenchmark-win_x64.exe`
- `resources.neu`
- `WebView2Loader.dll`

**Note**: Windows 10/11 includes WebView2 by default. For older Windows, users may need to install the [WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/).

## Project Structure

```
pc-benchmark/
├── neutralino.config.json    # App configuration
├── resources/
│   ├── index.html           # Main application
│   └── js/
│       └── neutralino.js    # Auto-downloaded by `neu update`
└── dist/                    # Built executables (after `neu build`)
```

## Customization

### Window Size
Edit `neutralino.config.json`:
```json
"modes": {
  "window": {
    "width": 950,
    "height": 800
  }
}
```

### App Name
Edit `neutralino.config.json`:
```json
"cli": {
  "binaryName": "YourAppName"
}
```

### Score Calibration
In `resources/index.html`, find `SCORE_CALIBRATION` object to adjust scoring thresholds for different hardware.

## Troubleshooting

### "neu: command not found"
Make sure npm global bin is in your PATH:
```bash
npm config get prefix
# Add that path + /bin to your PATH
```

### App won't start
- Ensure all 3 files are in the same folder (exe, resources.neu, dll)
- Try running as Administrator
- Check if WebView2 is installed

### Native features show "N/A"
- Running in browser mode (not as native app)
- Some features require Administrator privileges

## License
MIT - Feel free to modify and distribute.
