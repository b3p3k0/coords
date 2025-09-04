# coords

A simple Linux command-line tool to fetch GPS coordinates from gpsd and display them in multiple formats.

## Features

- **Multiple formats**: Display coordinates in decimal, DMS, JSON, UTM, or MGRS format
- **Flexible monitoring**: Single reading or continuous watching with customizable intervals
- **100% vibe coded**: Because I have a Claude subscription, so why not use it?

## Installation

```bash
# Create ~/.bin directory if it doesn't exist
mkdir -p ~/.bin

# Copy the coords executable and dependencies to your local bin directory
cp coords ~/.bin/
cp -r coords-deps ~/.bin/

# Add ~/.bin to your PATH if not already added
echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Test the installation
coords --help
```

## Prerequisites

- **gpsd**: Must be running and connected to your GPS hardware
- **Python 3**: Required for execution
- **an actual GPS dongle**: This shouldn't need to be said, but...

## Usage

### Basic Usage

```bash
# Show current coordinates (default: decimal format)
coords

# Get coordinates once and exit
coords --once

# Watch coordinates with default 10-second interval
coords --watch

# Watch coordinates with custom interval
coords --watch 30
```

### Output Formats

```bash
# Decimal degrees (default)
coords --format decimal
# Output: LAT: 35.106353, LON: -78.874085

# Degrees, Minutes, Seconds
coords --format dms  
# Output: LAT: 35°6'22.87"N, LON: 78°52'26.71"W

# JSON
coords --format json
# Output: {"lat": 35.106353, "lon": -78.874085}

# UTM coordinates
coords --format utm
# Output: Zone: 17S, Easting: 693740, Northing: 3886907

# Military Grid Reference System
coords --format mgrs
# Output: 17SPU9374086907
```

### Command Options

```
usage: coords [-h] [--format {decimal,dms,json,utm,mgrs}] [--once] [--watch [SECONDS]]

options:
  -h, --help            show this help message and exit
  --format {decimal,dms,json,utm,mgrs}
                        Output format (default: decimal)
  --once                Print one fix and exit
  --watch [SECONDS]     Continuously print fixes every SECONDS (default: 10, minimum: 1)
```

## Dependencies

All dependencies are included in the `coords-deps/` directory:
- **gpsd-py3**: Interface to gpsd daemon
- **utm**: Latitude/longitude to UTM coordinate conversion
- **mgrs**: Military Grid Reference System coordinate conversion
- **packaging**: Required by mgrs module

## License

GPL 3 see LICENSE for details.
