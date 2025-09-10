# Development and Testing Resources

This folder contains development and testing resources used during the automation creation process.

## Files

### `zonneplan_state.yaml`
**Sample Zonneplan sensor state data for testing**

This file contains a real example of the `sensor.zonneplan_current_electricity_tariff` state data, including:
- Current electricity prices (in micro-euros)
- Tariff groups (low/normal/high)
- 24+ hour forecast data
- Sustainability scores
- Solar yield data

**Purpose**: Used for testing template calculations and automation logic without needing live Zonneplan data.

**Usage**:
- Use in Home Assistant Developer Tools → Template to test price calculations
- Reference for understanding Zonneplan data structure
- Backup sample data for development and troubleshooting

**Data Structure**:
```yaml
forecast:
  - electricity_price: 782493        # Price in micro-euros (divide by 1,000,000)
    electricity_price_excl_tax: -446140  # Price excluding tax (use for calculations)
    tariff_group: low                # Rate tier: low/normal/high
    datetime: "2025-09-07T11:00:00.000000Z"  # UTC timestamp
    sustainability_score: 2450       # Environmental score
    solar_percentage: 0              # Solar energy percentage
    solar_yield: 0                   # Solar yield data
```

**Important Notes**:
- Prices are in micro-euros - divide by 1,000,000 for actual euro amounts
- Use `electricity_price_excl_tax` for cost calculations
- `datetime` field uses UTC timezone
- Forecast data typically contains 24-48 hours of future pricing

This data structure is essential for understanding how the automation templates parse and analyze Zonneplan pricing data to find optimal time windows.