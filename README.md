# Fractal Wildfire Visualization

An interactive browser-based visualization that simulates wildfire spread with fractal-like patterns. This project combines artistic visualization with educational elements about fire behavior.

Can also be found at: https://paladinindustries.com/Fire_Fractal.html

## Overview

This visualization uses HTML5 Canvas to render a real-time simulation of wildfire spreading across a landscape. The fire exhibits fractal-like behaviors, creating self-similar patterns at different scales. As the fire grows, the simulation automatically downsamples to maintain performance while preserving the visual appearance of continual growth.

## Features

- **Fractal Fire Patterns**: Creates emergent fractal-like patterns as fire spreads
- **Microphone Interaction**: Blow or make noise into your microphone to control wind intensity
- **Perspective View**: Click and drag to rotate the view and see the fire from different angles
- **Responsive Design**: Automatically adapts to browser window size
- **Continuous Growth**: Automatic downsampling allows the fire to grow indefinitely
- **Dynamic Visual Effects**: 
  - Wind-influenced flame direction
  - Ember particles at high wind speeds
  - Color transitions from golden terrain to crimson flames to black ash

## Controls

- **Mouse**: Click and drag to rotate the landscape
- **Microphone**: Make noise or blow to increase wind speed in the viewing direction
- **Visual Feedback**: A small circle in the top-left indicates microphone status (green when active)

## Technical Details

The simulation uses a grid-based cellular automaton approach with several enhancements:

- Fire spreads probabilistically based on neighbor state and wind direction
- Long-distance "jumps" create fractal-like patterns, more frequent with higher wind
- As fire approaches grid boundaries, the simulation expands the domain
- When the domain gets too large, downsampling occurs to maintain performance
- Visual scaling is carefully managed to keep the fire at a visible size

## Configuration Options

You can adjust several parameters to customize the visualization:

### Grid & Scaling Parameters

```javascript
const MIN_GRID_SIZE = 50;      // Smallest allowable grid size
const MAX_GRID_SIZE = 300;     // Maximum grid size (for performance)
const INITIAL_CELL_SIZE = 8;   // Starting cell size in pixels
const MIN_CELL_SIZE = 4;       // Minimum cell size when scaling
```

### Downsampling Controls

```javascript
// In the downsampleFire() function:
if (downsampleCount <= 2) {
    targetCumulativeScale = cumulativeScale * scaleFactor;
} else {
    // Change 1.1 to adjust zoom factor after initial downsamples
    targetCumulativeScale = cumulativeScale * 1.1; 
}

// In the drawFireGrid() function:
const scaleAdjustment = Math.min(Math.sqrt(cumulativeScale), 2.5); // Max scaling cap
```

### Fire Spread Parameters

```javascript
const WIND_AMPLIFICATION = 1.5;   // How much volume affects wind intensity
const SPREAD_BASE_PROB = 0.12;    // Base probability for fire spread
const SPREAD_WIND_MULT = 5.0;     // How wind increases spread in its direction
const JUMP_PROBABILITY = 0.02;    // Base probability for fire jumps
const JUMP_WIND_MULT = 8.0;       // How wind increases jump probability
const MAX_JUMP_DISTANCE = 6;      // Maximum jump distance
```

## Browser Requirements

This visualization uses modern web technologies including:
- HTML5 Canvas
- JavaScript ES6
- Web Audio API (for microphone input)

For best performance, use a recent version of Chrome, Firefox, Safari, or Edge.

## Performance Notes

The simulation is designed to run efficiently on modern computers, but performance may vary. If you experience lag:

1. Reduce `MAX_GRID_SIZE` to a lower value (e.g., 200)
2. Increase the downsampling frequency by lowering the `DOWNSAMPLE_THRESHOLD` value
3. Close other browser tabs and applications

## Future Enhancements

Potential areas for further development:
- Add terrain features that affect fire spread
- Implement smoke and atmospheric effects
- Add controls for adjusting parameters in real-time
- Incorporate real fire spread models from forestry science

## License

MIT License - Feel free to use, modify, and distribute this code for personal or educational purposes.