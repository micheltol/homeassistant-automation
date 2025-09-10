# Hottub Cost Optimization - Requirements Document

## Status: ✅ COMPLETED
This feature has been successfully implemented. See `hottub_cheapest_hours_automation.yaml` and `README.md` for the working solution.

## Original Goal
The goal of this automation is to reduce my electricity bill. I want to achieve this by running the pump for my hottub for the cheapest rates possible. 

## Required components

### Zonneplan

* Zonneplan is my electricity supplier
* the electricity rates change per hour (dynamic contract). Everyday 1300 CET the electricity rates for the next day will become available.
* there is an unofficial integration in home assistant which I have already installed via HACS: https://github.com/fsaris/home-assistant-zonneplan-one - via this integration you can fetch the hourly rates.

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

### hottub

My hottub is not smart; you can't control it via external integrations. So I plugged in a smart switch. [https://www.zigbee2mqtt.io/devices/HG06619.html#lidl-hg06619](https://www.zigbee2mqtt.io/devices/HG06619.html#lidl-hg06619)
* It can be  switched on/off  via zigbee (home assistant id: `switch.hottub_pomp`)

### Flow

* Read how long the hottub has to run from the home assistant helper `timer.hottub_timer`. If there is a broken hour - like 01:30:00 (1.5 hour) round the time up.
* At 2300 hours Determine for the next day when it is the cheapest to run for the consecutive hours
* plan the task for the next day
* When the hottub pump start the timer (`switch.hottub_pomp`) should start
* When the timer (`switch.hottub_pomp`) finishes the hottub pump switch should be turned off

### My current automation

My current automation just works on timer (every day at 11:00 hours) - I would like to update this automation to comply with my new requirements

```yaml

alias: Hottub pomp aan voor 2 uur (11:00)
description: ""
triggers:
  - at: "11:00:00"
    id: hotttub_on_time
    trigger: time
  - event_type: timer.finished
    event_data:
      entity_id: timer.hottub_timer
    id: hotttub_off
    trigger: event
  - entity_id: switch.hottub_pomp
    to: "on"
    id: Hottub_pump_on
    trigger: state
conditions: []
actions:
  - choose:
      - conditions:
          - condition: trigger
            id:
              - hotttub_on_time
        sequence:
          - action: switch.turn_on
            target:
              entity_id: switch.hottub_pomp
          - data: {}
            target:
              entity_id: timer.hottub_timer
            action: timer.start
            enabled: true
      - conditions:
          - condition: trigger
            id:
              - hotttub_off
        sequence:
          - action: switch.turn_off
            target:
              entity_id: switch.hottub_pomp
      - conditions:
          - condition: trigger
            id:
              - Hottub_pump_on
        sequence:
          - action: timer.start
            metadata: {}
            data: {}
            target:
              entity_id: timer.hottub_timer
mode: parallel
max: 3

```

## Implementation Summary

**Status**: ✅ Fully Implemented and Tested

**Key Features Delivered**:
- ✅ Daily scheduling at 23:05 for next day optimization
- ✅ Template-based precise timing execution  
- ✅ Configurable pump duration via timer helper
- ✅ Manual override with immediate timer start
- ✅ Automatic pump shutdown when timer expires
- ✅ Comprehensive logging and monitoring

**Files Created**:
- `hottub_cheapest_hours_automation.yaml` - Complete automation
- `README.md` - Installation and troubleshooting guide
- `REQUIREMENTS.md` - This requirements document

**Helper Requirements Met**:
- `timer.hottub_timer` - Configurable pump duration
- `input_datetime.hottub_start_time` - Calculated optimal start time storage

**Key Improvements Over Original Design**:
- Simplified triggers using template triggers instead of complex time-based logic
- More reliable execution timing
- Better integration with Home Assistant helper patterns
- Enhanced manual override detection

All original requirements have been successfully implemented with improvements for reliability and maintainability.