[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg?style=flat-square)](https://github.com/hacs/integration)
[![release][release-badge]][release-url]

[![Support the author on Patreon][patreon-shield]][patreon]

[![Buy me a coffee][buymeacoffee-shield]][buymeacoffee]

[patreon-shield]: https://frenck.dev/wp-content/uploads/2019/12/patreon.png
[patreon]: https://www.patreon.com/dutchdatadude

[buymeacoffee]: https://www.buymeacoffee.com/dutchdatadude
[buymeacoffee-shield]: https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png
[release-url]: https://github.com/jeroenterheerdt/HASmartIrrigation/releases
[release-badge]: https://img.shields.io/github/v/release/jeroenterheerdt/HASmartIrrigation?style=flat-square
# Smart Irrigation

![](logo.png?raw=true)

```diff
- WARNING: upgrading from V1 (V0.0.X) to V2 (V2023.X.X)? Read the instructions below!
```

| :warning: WARNING Are you upgrading from v0.0.X (aka V1) to V2023.X.X (aka V2)? |
|:---------------------------|
| Stop what you're doing and [capture your V1 configuration](https://jeroenterheerdt.github.io/HAsmartirrigation/installation-migration.html) _before_ installing V2. V2 is a complete overhaul of this integration and there is no upgrade path. This means that effectively you will have to start over. See the [docs](https://jeroenterheerdt.github.io/HAsmartirrigation/installation-migration.html) for instructions. We will not be able to recover your V1 configuration if you don't capture it before installing V2. |

This integration calculates the time to run your irrigation system to compensate for moisture loss by [evapotranspiration](https://en.wikipedia.org/wiki/Evapotranspiration). Using this integration you water your garden, lawn or crops precisely enough to compensate what has evaporated. It takes into account precipitation (rain, snow) and moisture loss caused by evapotranspiration and adjusts accordingly.
If it rains or snows less than the amount of moisture lost, then irrigation is required. Otherwise, no irrigation is required.
The integration can take into account weather forecasts for the coming days and also keeps track of the total moisture lost or added ('bucket')
Multiple zones are supported with each zone having it own configuration and set up.

## New Feature: 12-Month Watering Calendar

Smart Irrigation now includes a monthly watering calendar feature that generates yearly watering estimates for each irrigation zone. This feature uses representative climate data and your configured evapotranspiration calculation methods to provide planning insights.

### API Usage

**REST API:**
```
GET /api/smart_irrigation/watering_calendar
GET /api/smart_irrigation/watering_calendar?zone_id=1
```

**WebSocket API:**
```json
{
  "type": "smart_irrigation/watering_calendar",
  "zone_id": "1"  // optional, omit for all zones
}
```

### Features

- **Climate-Based Estimates**: Uses representative monthly climate data based on geographic location
- **Multiple Calculation Methods**: Supports PyETO (FAO-56), Thornthwaite, Static, and Passthrough methods  
- **Zone-Specific Calculations**: Accounts for zone size, multiplier, and other configuration parameters
- **Graceful Error Handling**: Continues processing other zones even if individual calculations fail
- **Seasonal Variation**: Automatically adjusts estimates based on latitude and seasonal patterns

*This feature addresses issue #579 and provides valuable planning information for irrigation scheduling.*

## Development

For contributors and developers:

### Quick Setup

```bash
# Clone and setup development environment
git clone <repository-url>
cd HAsmartirrigation
make setup
```

### Available Commands

```bash
make help        # Show all available commands
make test        # Run all tests
make test-knmi   # Test KNMI integration
make format      # Format code
make lint        # Run linting
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed development instructions.

## Read the docs: https://jeroenterheerdt.github.io/HAsmartirrigation/
