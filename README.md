# moco-palette

A web-based visualization system that connects to DragonFrame via OSC (Open Sound Control) and displays motion control data with interactive animations. Colored rectangles rotate into view based on the position of motion control axes.

![DragonFrame OSC Visualization Interface](client/palette-overview-small.png)

## Overview

This project creates a bridge between DragonFrame (a professional stop-motion animation software) and a web browser, allowing real-time visualization of motion control data. It consists of:

1. A Node.js server that receives OSC messages from DragonFrame
2. A WebSocket connection that forwards these messages to the browser
3. A web interface with dynamic animations that respond to the motion control axis values

The visualization shows a series of rotating colored rectangles that animate based on the position of motion control axes (particularly AX1).

## Features

- Real-time connection to DragonFrame via OSC
- WebSocket-based communication between server and client
- Dynamic visualization of motion control data
- Support for multiple axes
- Manual control slider for testing and demonstrations
- Auto-reconnection if the connection is lost
- Clean, modern UI with GSAP animations

## Prerequisites

- [Node.js](https://nodejs.org/) (v14 or higher recommended)
- [DragonFrame](https://www.dragonframe.com/) with OSC output enabled
- Modern web browser (Chrome, Firefox, Safari, or Edge)

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/ollygadiot/moco-palette.git
   cd moco-palette
   ```

2. Install server dependencies:
   ```
   cd server
   npm install
   ```

3. Configure DragonFrame:
   - Open DragonFrame
   - Go to Preferences > Advanced
   - Enable "Send OSC" and set the port to 7000 (default)
   - Set the OSC destination to 127.0.0.1

## Usage

1. Start the server:
   ```
   cd server
   npm start
   ```

2. Open the client in your web browser:
   - Open `client/index.html` in your browser

3. The web interface will connect to the server and display "Connected to DragonFrame bridge" when ready.

4. Move the motion control axes in DragonFrame to see the visualization respond, or use the manual slider for testing.

## Configuration

- **OSC Port**: By default, the server listens on port 7000 for DragonFrame OSC messages. You can modify this in `server.js`.
- **WebSocket Port**: The WebSocket server runs on port 9099. You can modify this in `server.js` and `client.js`.

## How It Works

1. DragonFrame sends OSC messages to the Node.js server when motion control axes are moved.
2. The server forwards these messages via WebSocket to the connected web clients.
3. The client JavaScript processes these messages and updates the visualization accordingly.
4. For AX1 specifically, the normalized value (0-1) controls how many of the 12 colored rectangles are displayed.

## Project Structure

```
moco-palette/
├── client/
│   ├── index.html              # Web client UI
│   ├── client.js               # Client-side JavaScript
│   └── palette-overview-small.png  # Screenshot
└── server/
    ├── package.json            # Node.js dependencies
    └── server.js               # OSC/WebSocket server
```

## Dependencies

**Server (Node.js):**
- `node-osc` (^9.1.5) - OSC protocol communication
- `ws` (^8.18.2) - WebSocket server

**Client (loaded via CDN):**
- GSAP 3.12.5 - Animation library

## Troubleshooting

**Server won't start:**
- Ensure port 7000 (OSC) and 9099 (WebSocket) are not in use by other applications
- Check that Node.js is installed correctly with `node --version`

**No OSC messages received:**
- Verify DragonFrame is configured to send OSC to `127.0.0.1:7000`
- Check that "Send OSC" is enabled in DragonFrame preferences
- Ensure the motion control axes are moving (check DragonFrame's motion control window)

**Client shows "Connecting..." indefinitely:**
- Make sure the server is running (`npm start` in the server directory)
- Check browser console for WebSocket connection errors
- Verify no firewall is blocking localhost connections

**Rectangles not animating:**
- The visualization responds specifically to the AX1 axis
- Use the manual slider to test if animations work independently of DragonFrame

## License

ISC License

## Author

Olly Gadiot

## Acknowledgements
[Graphics are based on the Palette Wallpaper pack by Oliur](https://store.oliur.com/b/palette-wallpaper-pack)
