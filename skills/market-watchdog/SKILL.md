# Market Watchdog Skill

## Overview
Automated market monitoring and trading execution for NVDA and PLTR.

## Data Store
Intelligence and technical data are stored in: [MARKET_INTEL.md](./MARKET_INTEL.md)

## Strategy
- **Aggressive Mode**: Enabled (Feb 4, 2026). 10-minute scan frequency during market hours.
- **Decision Logic**: Use `stock_analyze` and `stock_quote`. Focus on Momentum and dip-buying.
