# Home Assistant Electricity Cost Optimization Automations

This Home Assistant automation project optimizes appliance electricity costs by automatically scheduling operations during the cheapest electricity rate windows using dynamic pricing from Zonneplan. The project includes working automations for washing machine and hottub pump optimization.

## Project Structure

The project is organized into feature-specific folders:

### 📁 `washing-machine/`
**Real-time cost optimization for washing machines**
- MQTT button trigger activates cost optimization
- Finds optimal time within next 12 hours from trigger
- Manual override and immediate start capabilities
- See: [washing-machine/README.md](washing-machine/README.md)

### 📁 `hottub/`
**Daily scheduled optimization for hottub pumps**
- Calculates cheapest hours for next day at 23:05 daily
- Template-based precise execution timing
- Timer-based operation with configurable duration
- See: [hottub/README.md](hottub/README.md)

## Prerequisites

- **Home Assistant** with admin access
- **Zonneplan Integration** installed via HACS ([github.com/fsaris/home-assistant-zonneplan-one](https://github.com/fsaris/home-assistant-zonneplan-one))
- **Smart switches** controlling your appliances (Zigbee2MQTT recommended)
- **MQTT integration** for button functionality (if using washing machine automation)

## Quick Start

1. **Choose your automation**:
   - [Washing Machine](washing-machine/README.md) - Real-time optimization
   - [Hottub Pump](hottub/README.md) - Daily scheduled optimization

2. **Follow the specific README** in each folder for detailed installation steps

3. **Verify prerequisites**:
   - Zonneplan sensor: `sensor.zonneplan_current_electricity_tariff`
   - Smart switch entities for your appliances
   - MQTT button functionality (for washing machine)

## Key Features

### Common Features
- **Zonneplan Integration**: Uses dynamic electricity pricing data
- **Manual Override**: Always allows immediate manual control
- **Comprehensive Logging**: Detailed system logs for monitoring
- **Template Triggers**: Precise timing execution

### Washing Machine Specific
- **Button Trigger**: MQTT button press activation
- **Flexible Timing**: Optimizes within 12 hours from trigger
- **Immediate Fallback**: Starts immediately if optimal time is within 5 minutes
- **Timer Override**: Button press during active timer starts immediately

### Hottub Specific
- **Daily Planning**: Calculates next day's optimal schedule
- **Configurable Duration**: Set pump runtime via Home Assistant helpers
- **Predictable Schedule**: Consistent daily optimization

## Project Organization

The repository is organized into feature-specific folders for easy navigation:

```
📁 washing-machine/          # Real-time optimization
├── README.md               # Setup guide
├── REQUIREMENTS.md         # Original specs + implementation 
└── washing_machine_cheapest_hours_automation.yaml

📁 hottub/                  # Daily scheduled optimization  
├── README.md               # Setup guide
├── REQUIREMENTS.md         # Original specs + implementation
└── hottub_cheapest_hours_automation.yaml

📁 development/             # Testing resources
├── README.md               # Explains development files
└── zonneplan_state.yaml    # Sample data for testing
```

## Getting Started

1. **Choose your automation** based on your needs:
   - **Washing Machine**: Button press triggers optimization, delays to cheapest 3-hour window
   - **Hottub**: Plans daily schedule for next day's cheapest hours

2. **Navigate to the feature folder** and follow the README.md for complete setup instructions

3. **Prerequisites**: 
   - Home Assistant with Zonneplan integration
   - Smart switches for your appliances
   - MQTT integration for button functionality (washing machine only)

## Support

Each feature folder is self-contained with:
- ✅ Complete automation YAML files ready to use
- ✅ Step-by-step installation instructions  
- ✅ Comprehensive troubleshooting guides
- ✅ Helper entity creation steps
- ✅ Original requirements and implementation notes

**No additional configuration files needed** - everything works with Home Assistant's built-in helpers and the provided automation files.