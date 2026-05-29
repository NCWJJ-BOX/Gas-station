# Gas Station Simulator

Gas station simulator with web interface for ordering fuel and ESP8266 Arduino for controlling physical pump hardware.

## Architecture

```
Web Form (Browser)
    │ POST
    ▼
FastAPI Server
    │ GET /data
    ▼
ESP8266 (NodeMCU)
    │
    ├── 5x LCD I2C (display fuel info)
    └── Relay (pump control)
```

## Features

- Web form for selecting fuel type (91, 95, benzine) and quantity
- Automatic price calculation and summary
- QR code generation for mobile access
- Arduino polls API endpoint for latest order
- LCD display on Arduino showing fuel info
- Relay-controlled pump actuation

## Tech Stack

- **Backend:** Python FastAPI, Jinja2, Pydantic
- **Hardware:** ESP8266 (NodeMCU), 5x LCD I2C 16x2, push button, relay module
- **QR:** qrcode library

## Project Structure

```
Gas-station/
├── main.py                 # FastAPI entry point
├── backend/
│   ├── routes.py           # API routes (form, submit, data, qr-code)
│   ├── models.py           # Pydantic models
│   └── data_store.py       # In-memory data store
├── QRCode/
│   ├── QRCode.ino          # Arduino main sketch
│   ├── config.h            # WiFi and API config
│   ├── LCDManager.h        # LCD display handler
│   ├── DataFetcher.h       # HTTP data fetcher
│   └── PumpController.h    # Relay pump control
├── templates/
│   ├── form.html           # Fuel ordering form
│   └── qr_code.html        # QR code display page
└── requirements.txt
```

## Setup

```bash
pip install -r requirements.txt
python main.py
```

- Form: `http://localhost:8000/`
- QR Code: `http://localhost:8000/qr-code`

### Arduino

1. Open `QRCode/QRCode.ino` in Arduino IDE
2. Configure WiFi and server IP in `config.h`
3. Flash to ESP8266
