# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Home Assistant automation project focused on creating smart electricity cost optimization automations. The project includes working automations for both washing machine and hottub pump, automatically running appliances during the cheapest electricity rate periods using dynamic pricing data from the Zonneplan energy provider.

## Key Components and Integrations

### Zonneplan Integration
- Uses the unofficial Home Assistant integration: https://github.com/fsaris/home-assistant-zonneplan-one
- Main sensor: `sensor.zonneplan_current_electricity_tariff`
- Provides hourly electricity rates with forecast data (24+ hours ahead)
- Rate updates available daily at 13:00 CET
- Data includes electricity prices, tariff groups (low/normal/high), and sustainability scores

### Smart Appliance Control

#### Washing Machine
- Smart switch entity: `switch.wasmachine` (Zigbee2MQTT TS011F plug)
- Power monitoring sensor: `sensor.wasmachine_power`
- Power consumption thresholds:
  - Above 20W: Washing cycle active
  - Below 6W for 2+ minutes: Cycle finished
- Manual override capability by switching on the smart plug

#### Hottub Pump
- Smart switch entity: `switch.hottub_pomp`
- Timer-based operation (configurable duration)
- Manual override capability by switching on the smart plug

## Automation Logic Requirements

When creating automations for this project:

### Washing Machine Automation
1. **Cost Optimization**: Find the cheapest consecutive 3-hour blocks within the next 12 hours from trigger time
2. **Automatic Control**: Switch off appliance immediately when power > 20W detected, set timer for optimal period
3. **Manual Override**: Detect manual switch-on and reset automation timers
4. **Completion Detection**: Monitor power consumption to detect cycle completion (< 6W for 2+ minutes)
5. **Timer Management**: Use Home Assistant helper entities for countdown timers

### Hottub Pump Automation
1. **Daily Scheduling**: Calculate cheapest consecutive hours for next day at 23:05
2. **Timer-based Operation**: Use fixed timer duration (configurable via helper)
3. **Template Triggers**: Use template triggers for precise start time execution
4. **Manual Override**: Detect manual switch-on and start timer immediately

## Home Assistant Development Standards

- All automations should use YAML format
- Entity naming follows the pattern: `[device_name]_[property]`
- Use template sensors for complex calculations
- Implement proper condition checks before actions
- Include meaningful automation descriptions and aliases
- Use device triggers where available for better performance

## Project Structure

This is a development repository organized by feature with complete working Home Assistant automations:

### Feature Folders
- `washing-machine/` - Real-time washing machine cost optimization
  - `README.md` - Complete setup and troubleshooting guide
  - `REQUIREMENTS.md` - Original specifications and implementation summary
  - `washing_machine_cheapest_hours_automation.yaml` - Main automation

- `hottub/` - Daily scheduled hottub pump optimization  
  - `README.md` - Complete setup and troubleshooting guide
  - `REQUIREMENTS.md` - Original specifications and implementation summary
  - `hottub_cheapest_hours_automation.yaml` - Main automation

### Development Resources
- `development/` - Testing and development resources
  - `README.md` - Explains development files
  - `zonneplan_state.yaml` - Sample Zonneplan sensor data for testing

### Project Documentation
- `CLAUDE.md` - This development guidance document
- `README.md` - Main project overview and quick start guide

## Energy Rate Analysis

When working with Zonneplan data:
- Electricity prices are in micro-euros (divide by 1,000,000 for actual rate)
- Use `electricity_price_excl_tax` for calculations
- `tariff_group` indicates rate tiers: low, normal, high
- Forecast array provides 24+ hours of future pricing
- Consider sustainability_score for eco-friendly scheduling options