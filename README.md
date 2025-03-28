# Engineish

A THREE.js middleware that provides ROBLOX-like scripting capabilities for creating 3D games and experiences.

## Features

- Spawn characters with customizable models
- Create and manipulate basic geometric shapes (boxes, spheres, cylinders, cones, trusses)
- Organize objects using folders and groups
- Set properties like position, rotation, scale, and color
- Built-in optional multiplayer support with Socket.IO
- Scriptable and extensible architecture

## Installation

1. Clone the repository
2. Install dependencies:
```bash
npm install
```

## Development

The project uses Webpack for bundling and Babel for transpilation. Available scripts:

- `npm start`: Start the development server with hot reloading
- `npm run build`: Build for production
- `npm run server`: Start the multiplayer server
- `npm run dev`: Start both development server and multiplayer server concurrently

## Dependencies

### Core Dependencies
- three.js (^0.162.0): 3D graphics library
- socket.io-client (^4.7.4): Client-side multiplayer support
- express (^4.18.2): Server framework
- socket.io (^4.7.4): Server-side multiplayer support

### Development Dependencies
- webpack (^5.90.3): Module bundler
- babel (^7.24.0): JavaScript transpiler
- concurrently (^8.2.2): Run multiple commands concurrently

## Usage (The code in this section is under the CC0)

### Basic Setup

```html
<!DOCTYPE html>
<html>
<head>
  <title>Engineish</title>
</head>
<body>
<div id="engineish-container" width="80%" height="84%"></div>
<script src="bundle.js"></script>
<script>
    // Initialize the engine
    const engine = new Engine(document.getElementById('game-container'));
</script>
</body>
</html>
```

### Creating Parts

```javascript
// Create a box
const box = new Part('box', {
    width: 2,
    height: 1,
    depth: 2,
    color: 0xff0000
});

// Set position
box.setPosition(0, 1, 0);

// Set rotation
box.setRotation(0, Math.PI / 4, 0);

// Set scale
box.setScale(1, 1, 1);

// Add to workspace
engine.workspace.add(box);
```

### Spawning a Character

```javascript
// Spawn the default character
const player = engine.spawn();

// Set character position
player.setPosition(0, 5, 0);
```

### Creating Groups

```javascript
// Create a group
const house = engine.createGroup('House');

// Add parts to the group
house.add(walls);
house.add(roof);

// Manipulate the entire group
house.setPosition(0, 0, 0);
house.setRotation(0, Math.PI / 2, 0);
```

### Using Folders

```javascript
// Create a folder
const myFolder = engine.createFolder('MyFolder');

// Add objects to the folder
myFolder.add(house);
myFolder.add(box);

// Find objects in the folder
const found = myFolder.find('House');
```

### Adding a Baseplate

```javascript
// Add a baseplate with custom color
engine.addBaseplate(0x808080);
```

### Multiplayer Support

```javascript
// Connect to the multiplayer server
engine.connect('http://localhost:3000');

// Spawn a networked character
const player = engine.spawn({
    networked: true,
    position: { x: 0, y: 5, z: 0 }
});

// Sync object properties across network
player.sync({
    position: true,
    rotation: true,
    scale: true
});
```

## Available Part Types

- `box`: Rectangular prism
- `sphere`: Perfect sphere
- `cylinder`: Cylindrical shape
- `cone`: Conical shape
- `truss`: Simple truss structure

## Properties

All parts and groups support the following properties:

- `setPosition(x, y, z)`: Set the position in 3D space
- `setRotation(x, y, z)`: Set the rotation in radians
- `setScale(x, y, z)`: Set the scale in all dimensions
- `setColor(color)`: Set the color (hex value)

## License

SPL-R5 EX (New to this codebase.)