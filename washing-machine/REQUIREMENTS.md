# Washing Machine Cost Optimization - Requirements Document

## Status: ✅ COMPLETED
This feature has been successfully implemented. See `washing_machine_cheapest_hours_automation.yaml` and `README.md` for the working solution.

## Original Goal
The goal of this automation is to reduce electricity bills by running the washing machine during the cheapest electricity rate periods using dynamic pricing data. 

## Required components

### Zonneplan

* Zonneplan is my electricity supplier
* the electricity rates change per hour (dynamic contract). Everyday 1300 CET the electricity rates for the next day will become available.
* there is an unofficial integration in home assistant which I have already installed via HACS: https://github.com/fsaris/home-assistant-zonneplan-one - via this integration you can fetch the hourly rates.


sensor name: `sensor.zonneplan_current_electricity_tariff`

```
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
  - electricity_price: 2867444
    electricity_price_excl_tax: 1638810
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T05:00:00.000000Z"
    sustainability_score: 211
  - electricity_price: 2801620
    electricity_price_excl_tax: 1572986
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T06:00:00.000000Z"
    sustainability_score: 252
  - electricity_price: 2609472
    electricity_price_excl_tax: 1380838
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T07:00:00.000000Z"
    sustainability_score: 482
  - electricity_price: 2410185
    electricity_price_excl_tax: 1181551
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T08:00:00.000000Z"
    sustainability_score: 803
  - electricity_price: 2327784
    electricity_price_excl_tax: 1099150
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T09:00:00.000000Z"
    sustainability_score: 1222
  - electricity_price: 2279142
    electricity_price_excl_tax: 1050508
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T10:00:00.000000Z"
    sustainability_score: 1595
  - electricity_price: 2217916
    electricity_price_excl_tax: 989282
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T11:00:00.000000Z"
    sustainability_score: 1711
  - electricity_price: 2176776
    electricity_price_excl_tax: 948142
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T12:00:00.000000Z"
    sustainability_score: 1760
  - electricity_price: 2271761
    electricity_price_excl_tax: 1043127
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T13:00:00.000000Z"
    sustainability_score: 1635
  - electricity_price: 2360937
    electricity_price_excl_tax: 1132303
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T14:00:00.000000Z"
    sustainability_score: 1398
  - electricity_price: 2422164
    electricity_price_excl_tax: 1193530
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T15:00:00.000000Z"
    sustainability_score: 1127
  - electricity_price: 2712564
    electricity_price_excl_tax: 1483930
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T16:00:00.000000Z"
    sustainability_score: 760
  - electricity_price: 3243633
    electricity_price_excl_tax: 2014999
    tariff_group: high
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T17:00:00.000000Z"
    sustainability_score: 410
  - electricity_price: 3207575
    electricity_price_excl_tax: 1978941
    tariff_group: high
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T18:00:00.000000Z"
    sustainability_score: 152
  - electricity_price: 2836226
    electricity_price_excl_tax: 1607592
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T19:00:00.000000Z"
    sustainability_score: 39
  - electricity_price: 2721034
    electricity_price_excl_tax: 1492400
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T20:00:00.000000Z"
    sustainability_score: 29
  - electricity_price: 2637907
    electricity_price_excl_tax: 1409273
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T21:00:00.000000Z"
    sustainability_score: 25
  - electricity_price: 2603180
    electricity_price_excl_tax: 1374546
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T22:00:00.000000Z"
    sustainability_score: 26
  - electricity_price: 2560709
    electricity_price_excl_tax: 1332075
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-05T23:00:00.000000Z"
    sustainability_score: 28
  - electricity_price: 2517028
    electricity_price_excl_tax: 1288394
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T00:00:00.000000Z"
    sustainability_score: 25
  - electricity_price: 2467176
    electricity_price_excl_tax: 1238542
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T01:00:00.000000Z"
    sustainability_score: 29
  - electricity_price: 2448905
    electricity_price_excl_tax: 1220271
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T02:00:00.000000Z"
    sustainability_score: 32
  - electricity_price: 2469717
    electricity_price_excl_tax: 1241083
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T03:00:00.000000Z"
    sustainability_score: 39
  - electricity_price: 2612860
    electricity_price_excl_tax: 1384226
    gas_price: 11514157
    gas_price_excl_tax: 4518421
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T04:00:00.000000Z"
    sustainability_score: 43
  - electricity_price: 2645772
    electricity_price_excl_tax: 1417138
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T05:00:00.000000Z"
    sustainability_score: 53
  - electricity_price: 2498273
    electricity_price_excl_tax: 1269639
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T06:00:00.000000Z"
    sustainability_score: 128
  - electricity_price: 2262202
    electricity_price_excl_tax: 1033568
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T07:00:00.000000Z"
    sustainability_score: 391
  - electricity_price: 1546608
    electricity_price_excl_tax: 317974
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T08:00:00.000000Z"
    sustainability_score: 724
  - electricity_price: 1428633
    electricity_price_excl_tax: 199999
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T09:00:00.000000Z"
    sustainability_score: 1210
  - electricity_price: 1428391
    electricity_price_excl_tax: 199757
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T10:00:00.000000Z"
    sustainability_score: 1527
  - electricity_price: 1418227
    electricity_price_excl_tax: 189593
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T11:00:00.000000Z"
    sustainability_score: 1815
  - electricity_price: 1416654
    electricity_price_excl_tax: 188020
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T12:00:00.000000Z"
    sustainability_score: 1921
  - electricity_price: 1428512
    electricity_price_excl_tax: 199878
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T13:00:00.000000Z"
    sustainability_score: 1861
  - electricity_price: 1845357
    electricity_price_excl_tax: 616723
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T14:00:00.000000Z"
    sustainability_score: 1647
  - electricity_price: 2319072
    electricity_price_excl_tax: 1090438
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T15:00:00.000000Z"
    sustainability_score: 1372
  - electricity_price: 2745234
    electricity_price_excl_tax: 1516600
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T16:00:00.000000Z"
    sustainability_score: 974
  - electricity_price: 3210842
    electricity_price_excl_tax: 1982208
    tariff_group: high
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T17:00:00.000000Z"
    sustainability_score: 616
  - electricity_price: 3006715
    electricity_price_excl_tax: 1778081
    tariff_group: high
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T18:00:00.000000Z"
    sustainability_score: 438
  - electricity_price: 2657629
    electricity_price_excl_tax: 1428995
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T19:00:00.000000Z"
    sustainability_score: 379
  - electricity_price: 2518843
    electricity_price_excl_tax: 1290209
    tariff_group: normal
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T20:00:00.000000Z"
    sustainability_score: 392
  - electricity_price: 2352105
    electricity_price_excl_tax: 1123471
    tariff_group: low
    solar_percentage: 0
    solar_yield: 0
    datetime: "2025-09-06T21:00:00.000000Z"
    sustainability_score: 400
unit_of_measurement: €/kWh
icon: mdi:cash
friendly_name: Zonneplan Current electricity tariff

```


### washing machine

My washing machine is not smart; you can;t control it via external integrations. So I plugged in a smart switch. https://www.zigbee2mqtt.io/devices/TS011F_plug_1.html 

* It can be  switched on/off  via zigbee (home assistant id: `switch.wasmachine`)
* You can read th e current power usage: (home assistant id: `wasmachine_power`)
* The washing machine needs to be turned on to open the frontdoor, select the program etc.

Based on the power usage we can determine if the washing machine is switched on and it's cleaning program started. 
If the washing machine power usage is below 20W we can assume it's switched on but not running.


### Flow
When I load the washing machine, I fill it up select the program and start it.
The automation should kick in when power consumption goes above 20W (washing cycle started) and determine for the next 12 hours from that moment - what the cheapest 3 consecutive hours are and switch the washing machine via the smartplug off. It sets a timer countdown helper (`timer.washing_machine_delay`) which counts down the time to the cheapest hours.
If the timer fires (the start of the cheapest hours), the automation should switch on the plug and the washing machine will run.

If we manually switch on the smart plug (after it got switched off by the automation) this means we want to use the washing machine now and don't want to wait for the cheapest hour. The timer should reset and nothing should happen.
The washing machine is finished if the power consumption was below 6W for 2 minutes.

### Technical Clarifications
- Timer helper: Use `timer.washing_machine_delay` (configuration included)
- Power sensor: `wasmachine_power` is already available
- Trigger: Automation triggers when power > 20W (washing cycle started)  
- Time window: 12 hours starts from the moment washing machine is detected as started
- Consecutive hours: Must be exactly 3 consecutive hours for optimal pricing
- Edge cases:
  - If washing machine starts very close to optimal time window: Just start immediately
  - Rates are updated daily at 13:00 CET and remain static until next update
  - Forecast data availability: Since rates for the entire next day are published at 13:00 CET, there will always be sufficient forecast data (minimum 12+ hours) regardless of when the washing machine is started

## Implementation Summary

**Status**: ✅ Fully Implemented and Tested

**Key Features Delivered**:
- ✅ Power-based detection (>20W trigger, <6W completion)
- ✅ Real-time optimization within 12-hour window from start
- ✅ Automatic machine shutdown and timer-based restart
- ✅ Manual override capability with timer cancellation
- ✅ Template-based precise timing execution
- ✅ Comprehensive logging and monitoring
- ✅ Edge case handling (immediate start if optimal time <5min)

**Files Created**:
- `washing_machine_cheapest_hours_automation.yaml` - Complete automation
- `README.md` - Installation and troubleshooting guide
- `REQUIREMENTS.md` - This requirements document

**Helper Requirements Met**:
- `timer.washing_machine_delay` - Dynamic countdown timer
- `input_datetime.washing_machine_start_time` - Calculated optimal start time storage

All original requirements have been successfully implemented and tested.

