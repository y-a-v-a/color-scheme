# Color Scheme

A modern ES Module for generating harmonious color schemes with extended functionality. Based on the original color-scheme-js by c0bra, this module provides an extensive set of color harmony algorithms and advanced features for creating beautiful color palettes.

## Features

- **16 Built-in Color Schemes**: From basic monochromatic to advanced perlin noise-based schemes
- **Flexible Color Count**: Generate 2-16 colors per scheme
- **Color Variations**: Each color comes with 4 variations (different brightness/saturation levels)
- **Method Chaining**: Fluent API for easy configuration
- **Modern ES Modules**: Full ES6+ module support
- **Advanced Schemes**: Includes golden ratio, seasonal, gradient, and chaos schemes
- **Saturation Control**: Adjust saturation levels of generated colors
- **Web-Safe Colors**: Optional web-safe color generation
- **Comprehensive Testing**: Well-tested with included test suite

## Installation

```bash
npm install color-scheme
```

## Quick Start

```javascript
import ColorScheme from 'color-scheme';

// Create a basic color scheme
const scheme = new ColorScheme();
const colors = scheme
  .fromHue(120)           // Start with green
  .setScheme('tetrade')   // Use tetrade (4-color) scheme
  .getColors();          // Get array of hex colors

console.log(colors); // ['80ff80', '80ff40', 'a0ff60', 'c0ff80', ...]
```

## Available Color Schemes

### Basic Schemes
- **`mono`** / **`monochromatic`**: Single color with variations
- **`contrast`**: Base color + its complement (opposite on color wheel)
- **`triade`**: Three colors evenly distributed around color wheel (120° apart)
- **`tetrade`**: Four colors forming a rectangle on color wheel
- **`analogic`**: Adjacent colors on the color wheel
- **`splitComplement`**: Base color + two colors adjacent to its complement
- **`square`**: Four colors evenly spaced (90° apart)

### Advanced Schemes
- **`phi`**: Colors spaced by golden ratio angle (137.5°) - naturally harmonious
- **`shades`**: Progressively darker versions of base color
- **`tints`**: Progressively lighter versions of base color
- **`chaos`**: Semi-random colors with controlled relationship to base
- **`seasons`**: Colors inspired by seasonal transitions
- **`gradient`**: Linear transition between two colors
- **`perlin`**: Organic color variations using perlin-like noise

## API Reference

### Constructor

```javascript
const scheme = new ColorScheme(options);
```

**Options:**
- `colorCount` (number): Number of colors to generate (2-16, default: 4)

### Core Methods

#### `fromHue(hue)`
Set the base hue for the color scheme.
- `hue` (number): Hue value (0-359)
- Returns: ColorScheme instance for chaining

```javascript
scheme.fromHue(240); // Start with blue
```

#### `fromHex(hex)`
Set the base color from a hexadecimal color code.
- `hex` (string): Hex color code without # (e.g., 'FF0000')
- Returns: ColorScheme instance for chaining

```javascript
scheme.fromHex('FF6B35'); // Start with orange
```

#### `setScheme(name)`
Set the color harmony scheme to use.
- `name` (string): Scheme name (see available schemes above)
- Returns: ColorScheme instance for chaining

```javascript
scheme.setScheme('analogic');
```

#### `getColors()`
Generate and return the color scheme as hex codes.
- Returns: Array of hex color strings (without #)

```javascript
const colors = scheme.getColors();
// ['80ff80', '60ff60', '40ff40', '20ff20', ...]
```

#### `getColorSet()`
Get colors grouped by base color (4 variations per group).
- Returns: Array of arrays, each containing 4 color variations

```javascript
const colorSets = scheme.getColorSet();
// [['80ff80', '60ff60', '40ff40', '20ff20'], ['ff8080', ...], ...]
```

### Configuration Methods

#### `setColorCount(count)`
Set the number of base colors to generate.
- `count` (number): Number of colors (2-16)
- Returns: ColorScheme instance for chaining

```javascript
scheme.setColorCount(8);
```

#### `setDistance(distance)`
Set the distance between colors in applicable schemes.
- `distance` (number): Distance value (0-1)
- Returns: ColorScheme instance for chaining

```javascript
scheme.setDistance(0.3); // Closer colors
```

#### `setVariation(preset)`
Set the color variation preset.
- `preset` (string): Preset name ('default', 'pastel', 'soft', 'light', 'hard', 'pale', 'vibrant', 'muted')
- Returns: ColorScheme instance for chaining

```javascript
scheme.setVariation('pastel');
```

#### `setSeed(seed)`
Set random seed for noise-based schemes (chaos, perlin).
- `seed` (number): Seed value for deterministic randomness
- Returns: ColorScheme instance for chaining

```javascript
scheme.setSeed(12345);
```

### Saturation Control

#### `adjustSaturation(amount)`
Adjust saturation of all colors.
- `amount` (number): Adjustment amount (-1 to 1)
- Returns: ColorScheme instance for chaining

```javascript
scheme.adjustSaturation(0.3);  // More saturated
scheme.adjustSaturation(-0.5); // Less saturated
```

#### `saturate(amount)`
Increase saturation.
- `amount` (number): Amount to increase (0-1)
- Returns: ColorScheme instance for chaining

#### `desaturate(amount)`
Decrease saturation.
- `amount` (number): Amount to decrease (0-1)
- Returns: ColorScheme instance for chaining

### Additional Options

#### `addComplement(boolean)`
Add complementary color to analogic scheme.
- Returns: ColorScheme instance for chaining

```javascript
scheme.setScheme('analogic').addComplement(true);
```

#### `useWebSafe(boolean)`
Enable web-safe color generation.
- Returns: ColorScheme instance for chaining

```javascript
scheme.useWebSafe(true);
```

## Examples

### Basic Usage

```javascript
import ColorScheme from 'color-scheme';

// Monochromatic blue scheme
const monoBlue = new ColorScheme()
  .fromHue(240)
  .setScheme('mono')
  .getColors();

// Complementary orange scheme
const complementary = new ColorScheme()
  .fromHex('FF6B35')
  .setScheme('contrast')
  .getColors();
```

### Advanced Schemes

```javascript
// Golden ratio color harmony
const goldenColors = new ColorScheme()
  .fromHue(0)
  .setScheme('phi')
  .setColorCount(5)
  .getColors();

// Seasonal color palette
const seasonalColors = new ColorScheme()
  .fromHue(120)
  .setScheme('seasons')
  .getColors();

// Pastel gradient
const pastelGradient = new ColorScheme()
  .fromHue(300)
  .setScheme('gradient')
  .setVariation('pastel')
  .setColorCount(6)
  .getColors();
```

### Method Chaining

```javascript
const customScheme = new ColorScheme({ colorCount: 8 })
  .fromHue(180)
  .setScheme('tetrade')
  .setDistance(0.4)
  .setVariation('vibrant')
  .desaturate(0.2)
  .useWebSafe(false)
  .getColors();
```

### Working with Color Sets

```javascript
const scheme = new ColorScheme()
  .fromHue(60)
  .setScheme('triade');

// Get grouped colors (4 variations per base color)
const colorSets = scheme.getColorSet();

colorSets.forEach((set, index) => {
  console.log(`Color ${index + 1} variations:`, set);
  // Color 1 variations: ['ffff80', 'ffff60', 'ffff40', 'ffff20']
  // Color 2 variations: ['80ff80', '60ff60', '40ff40', '20ff20']
  // etc.
});
```

### Noise-Based Schemes

```javascript
// Perlin noise for organic color variations
const organicColors = new ColorScheme()
  .fromHue(150)
  .setScheme('perlin')
  .setSeed(42)
  .setColorCount(12)
  .getColors();

// Controlled chaos with seed for reproducibility
const chaosColors = new ColorScheme()
  .fromHue(270)
  .setScheme('chaos')
  .setSeed(12345)
  .getColors();
```

## Color Variations

Each base color in a scheme generates 4 variations with different brightness and saturation levels:
- **Variation 0**: Base color
- **Variation 1**: Darker version
- **Variation 2**: Lighter version  
- **Variation 3**: Muted version

These variations provide flexibility for creating cohesive designs with subtle differences.

## Presets

Available variation presets:
- **`default`**: Balanced variations
- **`pastel`**: Soft, muted colors
- **`soft`**: Gentle variations
- **`light`**: Bright, light colors
- **`hard`**: High contrast variations
- **`pale`**: Very light, washed-out colors
- **`vibrant`**: Highly saturated colors
- **`muted`**: Low saturation colors

## Browser Support

This module uses ES6+ features and requires:
- Node.js 14+
- Modern browsers with ES module support
- Build tools with ES module support (webpack, rollup, etc.)

## Testing

Run the included test suite:

```bash
npm test
```

## License

MIT

## Credits

Based on the original [color-scheme-js](https://github.com/c0bra/color-scheme-js) by c0bra, with significant extensions and modernization.