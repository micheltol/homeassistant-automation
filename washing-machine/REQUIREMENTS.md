# Washing Machine Cost Optimization - Requirements Document

## Status: ✅ COMPLETED (Updated September 2024)
This feature has been successfully implemented with MQTT button trigger approach. See `washing_machine_cheapest_hours_automation.yaml` and `README.md` for the current working solution.

## Goal
Reduce electricity bills by running the washing machine during the cheapest electricity rate periods using dynamic pricing data from Zonneplan.

## Required Components

### Zonneplan Integration
* Zonneplan is the electricity supplier
* Electricity rates change per hour (dynamic contract)
* Daily at 13:00 CET the electricity rates for the next day become available
* Unofficial Home Assistant integration installed via HACS: [https://github.com/fsaris/home-assistant-zonneplan-one](https://github.com/fsaris/home-assistant-zonneplan-one)

**Sensor:** `sensor.zonneplan_current_electricity_tariff`

**Sample Data Structure:**
```yaml
state_class: measurement
forecast:
  - electricity_price: 2711233
    electricity_price_excl_tax: 1482599
    gas_price: 11530235
    gas_price_excl_tax: 4534499
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T04:00:00.000000Z"
    sustainability_score: 215
  # ... (additional hourly forecast data)
unit_of_measurement: €/kWh
icon: mdi:cash
friendly_name: Zonneplan Current electricity tariff
```

### Washing Machine Setup
* Non-smart washing machine connected via smart switch
* Zigbee2MQTT TS011F smart plug: [https://www.zigbee2mqtt.io/devices/TS011F_plug_1.html](https://www.zigbee2mqtt.io/devices/TS011F_plug_1.html)
* Home Assistant switch entity: `switch.wasmachine`
* Smart switch with physical button functionality
* Button publishes MQTT messages to: `zigbee2mqtt/wasmachine switch/action`

## Implementation Approaches

### Current Implementation (MQTT Button Trigger)
**Status:** ✅ ACTIVE (September 2024)

**Trigger Method:** MQTT button press on smart switch
- Button topic: `zigbee2mqtt/wasmachine switch/action`
- Payloads: `single` or `double` (both trigger same behavior)

**Flow:**
1. User loads washing machine, selects program, and starts it
2. **User presses button on smart switch** to activate cost optimization
3. Automation switches OFF machine and calculates cheapest 3 consecutive hours within next 12 hours
4. Timer (`timer.washing_machine_delay`) counts down to optimal start time
5. When timer expires, automation switches ON machine to run during cheapest hours
6. **Edge Cases:**
   - Button press during active timer → Cancel timer + start immediately
   - Manual switch-on during timer → Cancel timer + keep running
   - Optimal time within 5 minutes → Start immediately

### Previous Implementation (Power Monitoring)
**Status:** ❌ DEPRECATED (Replaced September 2024)

**Trigger Method:** Power consumption monitoring
- Trigger: Power consumption > 20W (washing cycle started)
- Completion: Power < 6W for 2+ minutes
- **Issues:** Infinite loops, false completion detection, complex state management

## Technical Specifications

### Core Logic (Unchanged)
- **Time Window:** 12 hours from trigger moment
- **Consecutive Hours:** Exactly 3 consecutive hours for optimal pricing
- **Cost Calculation:** Uses `electricity_price_excl_tax` values from Zonneplan forecast
- **Algorithm:** Template-based iteration through forecast data to find minimum cost 3-hour block

### Home Assistant Helpers Required
**Current (MQTT Approach):**
- `timer.washing_machine_delay` - Countdown timer for optimal start time

**Previous (Power Monitoring Approach):**
- `timer.washing_machine_delay` - Countdown timer
- `input_boolean.washing_machine_automation_active` - State tracking (no longer needed)
- `input_datetime.washing_machine_start_time` - Start time storage (no longer needed)

### Edge Cases Handling
- **Immediate Start:** If optimal time is within 5 minutes, start immediately
- **Rate Updates:** Daily at 13:00 CET, sufficient forecast data always available (24+ hours)
- **Manual Override:** Always allows immediate manual control with timer cancellation
- **Timer Reset:** New button press during active timer cancels and starts immediately

## Implementation Files

### Current Files
- `washing_machine_cheapest_hours_automation.yaml` - MQTT button trigger automation
- `README.md` - Installation and troubleshooting guide  
- `REQUIREMENTS.md` - This requirements document

### Key Features Delivered
- ✅ MQTT button trigger activation
- ✅ Real-time optimization within 12-hour window
- ✅ Automatic machine shutdown and timer-based restart
- ✅ Manual override capability with timer cancellation
- ✅ Template-based precise timing execution
- ✅ Comprehensive logging and monitoring
- ✅ Edge case handling (immediate start, timer conflicts)
- ✅ Simplified helper requirements (only timer needed)

## Evolution Summary

**September 2024 Update:**
- **Replaced:** Power consumption triggers with MQTT button triggers
- **Simplified:** Reduced from 3 helpers to 1 helper
- **Fixed:** Infinite loop issues and false completion detection
- **Improved:** More reliable user control and predictable behavior
- **Enhanced:** Direct user intent capture via physical button press

The current MQTT button approach provides more reliable operation and better user experience compared to the previous power monitoring method.