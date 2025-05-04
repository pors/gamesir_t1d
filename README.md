# GameSir T1d Pygame Wrapper

A Python package that provides a Pygame-compatible interface for the GameSir T1d controller, making it easy to use in Pygame applications. This package handles BLE connections, reconnections, and provides a convenient API.

## Features

- Bluetooth Low Energy (BLE) connection to GameSir T1d controllers
- Automatic reconnection handling
- Pygame-compatible interface for easy integration
- Raw controller data access
- Mapped buttons and axes with proper normalization
- BLE scanner tool to discover controller names

## Installation

```bash
pip install gamesir-t1d
```

Or with uv:

```bash
uv add gamesir-t1d
```

## Finding Your Controller Name

Before using the package, you need to know your controller's exact name. Each GameSir T1d controller broadcasts with a name like "Gamesir-T1d-XXXX" where XXXX is a unique identifier.

Use the included scanner tool to discover your controller:

```bash
# After installing the package
gamesir-scan
```

Make sure your controller is turned on and in pairing mode (typically hold the power button until LEDs flash rapidly). The scanner will show all discovered Bluetooth devices and try to identify GameSir controllers.

The scanner has additional options:

```bash
# Skip the "Press Enter" prompt and start scanning immediately
gamesir-scan --no-prompt

# Adjust the scan timeout (in seconds)
gamesir-scan --timeout 5.0

# Get help on available options
gamesir-scan --help
```

## Basic Usage

```python
from gamesir_t1d import GameSirT1dPygame

# Create the controller object with your controller's name
controller = GameSirT1dPygame("Gamesir-T1d-XXXX")  # Replace XXXX with your controller ID

# Initialize the controller (starts BLE connection)
controller.init()

# Read axes and buttons using the pygame-compatible interface
left_x = controller.get_axis(0)  # Range: -1.0 to 1.0
left_y = controller.get_axis(1)  # Range: -1.0 to 1.0
a_button = controller.get_button(0)  # 1 for pressed, 0 for not pressed

# Check if the controller is connected
if controller.is_connected():
    print("Controller is connected!")

# Clean up when done
controller.quit()
```

## Pygame Example

The package includes an example Pygame application that demonstrates how to use the controller:

```python
# Assuming you've installed the package with the [examples] extra
# pip install gamesir-t1d[examples]
from gamesir_t1d.examples import run_example

# Run the demo
run_example("Gamesir-T1d-XXXX")  # Replace XXXX with your controller ID
```

Or you can run the example script directly:

```bash
python -m examples.pygame_example
```

## Button Mapping

- Axis 0: Left stick X (-1.0 to 1.0)
- Axis 1: Left stick Y (-1.0 to 1.0)
- Axis 2: Right stick X (-1.0 to 1.0)
- Axis 3: Right stick Y (-1.0 to 1.0)
- Button 0: A button
- Button 1: B button
- Button 2: X button
- Button 3: Y button
- Button 4: L1 button
- Button 5: R1 button
- Button 6: L2 button (digital)
- Button 7: R2 button (digital)
- Button 8: C1 button
- Button 9: C2 button
- Button 10: Menu button
- Hat 0: D-pad (returns a tuple of (x, y) where each can be -1, 0, or 1)

## License

MIT License - see the LICENSE file for details.