# Washing Machine Cost Optimization Automation

## Purpose
Automatically delays your washing machine to run during the cheapest 3-hour electricity rate period within the next 12 hours, using Zonneplan dynamic pricing data. This automation optimizes electricity costs by triggering via MQTT button press and rescheduling the washing machine for the most cost-effective time window.

## How It Works
1. **Trigger**: Press button on smart switch (single or double press)
2. **Analysis**: Finds cheapest 3 consecutive hours in next 12 hours
3. **Delay**: Switches off machine and sets timer for optimal start time
4. **Execution**: Automatically restarts at the cheapest time
5. **Override**: Manual switch-on cancels optimization
6. **Immediate Start**: Button press during active timer cancels timer and starts immediately

## Files
- `washing_machine_cheapest_hours_automation.yaml` - Main automation
- `README.md` - This setup guide

## Quick Installation

### Required Home Assistant Helpers
Create this helper in Settings → Devices & Services → Helpers:

1. **Timer**: `timer.washing_machine_delay`
   - Name: "Washing Machine Delay"
   - Duration: 12:00:00
   - **Restore state**: **OFF** (unchecked) - Allows fresh cost calculations after Home Assistant restarts

### Required Entities
Verify these entities exist:
- `switch.wasmachine` (smart plug with button functionality)
- `sensor.zonneplan_current_electricity_tariff` (Zonneplan integration)
- MQTT integration configured for Zigbee2MQTT
- Smart switch publishes to: `zigbee2mqtt/wasmachine switch/action`

### Installation Steps
1. Create the required helper (above)
2. Go to Settings → Automations & Scenes → Create Automation
3. Click "Skip" → Switch to YAML mode
4. Copy and paste the content from `washing_machine_cheapest_hours_automation.yaml`
5. Save the automation

## Button Actions
- **Single press**: Triggers cost optimization
- **Double press**: Triggers cost optimization (same behavior)
- **Manual switch-on**: Cancels timer and runs immediately

## Troubleshooting

### Common Issues
1. **Automation doesn't trigger**: 
   - Check MQTT integration is working
   - Verify button presses publish to `zigbee2mqtt/wasmachine switch/action`
   - Check MQTT payload is `single` or `double`

2. **MQTT not working**: 
   - Verify Zigbee2MQTT is running and connected
   - Check smart switch is properly paired
   - Test MQTT messages in Developer Tools → MQTT

3. **Timer doesn't start**: 
   - Verify `timer.washing_machine_delay` helper exists
   - Check Home Assistant logs for error messages

4. **No optimal time found**: 
   - Check that Zonneplan sensor has forecast data available
   - Verify `sensor.zonneplan_current_electricity_tariff` has forecast attribute

5. **Template errors**: 
   - Verify all entity names match your Home Assistant configuration
   - Check Developer Tools → Template to test calculations

### Monitoring
The automation includes comprehensive logging. Check Home Assistant logs for:
- "Washing machine delayed for X hours for cheapest 3-hour block" - Shows delay duration
- "Timer cancelled - washing machine started immediately" - Button press during active timer
- "Manual override - washing machine timer cancelled" - Manual switch detected  
- "Washing machine started at optimal time" - Timer expired, started washing machine

### Entity Customization
If your entity names differ, update these in the automation YAML:
- `switch.wasmachine` → your smart plug switch name
- `zigbee2mqtt/wasmachine switch/action` → your MQTT topic path
- Helper entities (if you used different names when creating them)

### MQTT Topic Configuration
The automation expects MQTT messages on topic: `zigbee2mqtt/wasmachine switch/action`
With payloads: `single` or `double`

If your Zigbee2MQTT uses different naming, update the MQTT trigger topics in the automation.