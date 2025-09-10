# Washing Machine Cost Optimization Automation

## Purpose
Automatically delays your washing machine to run during the cheapest 3-hour electricity rate period within the next 12 hours, using Zonneplan dynamic pricing data. This automation optimizes electricity costs by detecting when you start the washing machine and rescheduling it for the most cost-effective time window.

## How It Works
1. **Detection**: When power consumption > 20W (washing cycle started)
2. **Analysis**: Finds cheapest 3 consecutive hours in next 12 hours
3. **Delay**: Switches off machine and sets timer for optimal start time
4. **Execution**: Automatically restarts at the cheapest time
5. **Completion**: Detects cycle completion (power < 6W for 2+ minutes)
6. **Override**: Manual switch-on cancels optimization

## Files
- `washing_machine_cheapest_hours_automation.yaml` - Main automation
- `README.md` - This setup guide

## Quick Installation

### Required Home Assistant Helpers
Create these helpers in Settings → Devices & Services → Helpers:

1. **Timer**: `timer.washing_machine_delay`
   - Name: "Washing Machine Delay"
   - Duration: 12:00:00

2. **Input Datetime**: `input_datetime.washing_machine_start_time`
   - Name: "Washing Machine Start Time"
   - Enable both Date and Time

### Required Entities
Verify these entities exist:
- `sensor.wasmachine_power` (power monitoring)
- `switch.wasmachine` (smart plug)
- `sensor.zonneplan_current_electricity_tariff` (Zonneplan integration)

### Installation Steps
1. Create the required helpers (above)
2. Go to Settings → Automations & Scenes → Create Automation
3. Click "Skip" → Switch to YAML mode
4. Copy and paste the content from `washing_machine_cheapest_hours_automation.yaml`
5. Save the automation

## Power Thresholds
- **> 20W**: Washing cycle active
- **< 20W**: Machine on but standby
- **< 6W for 2+ minutes**: Cycle completed

## Troubleshooting

### Common Issues
1. **Automation doesn't trigger**: 
   - Check that `sensor.wasmachine_power` is reporting correct values
   - Verify power consumption actually exceeds 20W when washing starts

2. **Timer doesn't start**: 
   - Verify `timer.washing_machine_delay` helper exists
   - Check Home Assistant logs for error messages

3. **No optimal time found**: 
   - Check that Zonneplan sensor has forecast data available
   - Verify `sensor.zonneplan_current_electricity_tariff` has forecast attribute

4. **Template errors**: 
   - Verify all entity names match your Home Assistant configuration
   - Check Developer Tools → Template to test calculations

### Monitoring
The automation includes comprehensive logging. Check Home Assistant logs for:
- "Washing machine delayed until..." - Shows calculated optimal time
- "Manual override - washing machine timer cancelled" - Manual switch detected  
- "Washing machine started at optimal time" - Timer expired, started pump
- "Washing cycle completed..." - Power consumption below 6W threshold

### Entity Customization
If your entity names differ, update these in the automation YAML:
- `sensor.wasmachine_power` → your power sensor name
- `switch.wasmachine` → your smart plug switch name
- Helper entities (if you used different names when creating them)