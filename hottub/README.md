# Hottub Pump Cost Optimization Automation

## Purpose
Automatically schedules your hottub pump to run during the cheapest electricity rate periods for the next day. The automation calculates the optimal time window daily at 23:05 based on Zonneplan dynamic pricing data and starts the pump at the calculated cheapest time.

## How It Works
1. **Daily Planning**: Every day at 23:05, calculates cheapest consecutive hours for tomorrow
2. **Scheduling**: Sets the optimal start time in a datetime helper
3. **Execution**: Template trigger fires precisely at the scheduled time to start the pump
4. **Timer Control**: Runs for the duration specified in the timer helper
5. **Auto-stop**: Automatically switches off pump when timer expires
6. **Manual Override**: Manual switch-on starts timer immediately

## Files
- `hottub_cheapest_hours_automation.yaml` - Main automation

## Quick Installation

### Required Home Assistant Helpers
Create these helpers in Settings → Devices & Services → Helpers:

1. **Timer**: `timer.hottub_timer`
   - Name: "Hottub Timer"
   - Duration: Set your desired pump runtime (e.g., 02:00:00 for 2 hours)

2. **Input Datetime**: `input_datetime.hottub_start_time`
   - Name: "Hottub Start Time"
   - Enable both Date and Time

### Required Entities
Verify these entities exist:
- `switch.hottub_pomp` (smart switch controlling pump)
- `sensor.zonneplan_current_electricity_tariff` (Zonneplan integration)

### Installation Steps
1. Create the required helpers (above)
2. Go to Settings → Automations & Scenes → Create Automation
3. Click "Skip" → Switch to YAML mode
4. Copy and paste the content from `hottub_cheapest_hours_automation.yaml`
5. Save the automation

## Automation Logic
- **23:05 Daily**: Analyzes next day's rates and schedules optimal start time
- **Template Trigger**: Fires precisely when scheduled time arrives
- **Timer Management**: Starts timer when pump begins, stops pump when timer expires
- **Manual Override**: Manual activation starts timer immediately without rescheduling

## Customization
- Adjust timer duration in the `timer.hottub_timer` helper
- Change planning time by modifying the "23:05:00" trigger time
- Modify the cheapest hours calculation logic for different optimization strategies

The automation includes comprehensive logging to monitor daily scheduling and pump operation.