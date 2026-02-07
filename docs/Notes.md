
Chart Scaling System Prompt
Overview
Build a dual-axis financial chart where price is the base layer and all other metrics (scores, indicators) are visually scaled to overlay on the price chart for pattern correlation.

Core Concept
The left Y-axis domain is determined by the price range (min/max) of the asset. All non-price data is mathematically mapped onto this same domain so visual alignment reveals correlations.

Scaling Formula
scaledValue = minPrice + (value / 100) * priceRange

Where:
- minPrice = lowest price in the visible dataset
- priceRange = maxPrice - minPrice
- value = the 0-100 normalized metric (score, inverted VIX, etc.)
Data Type Handling
Data Type	Range	Scaling Method
Price	Varies	Direct plot (defines the domain)
Scores	0-100	Apply formula directly
VIX	~10-80	Invert first: 100 - vix, then apply formula
VIX Inversion Rationale
VIX moves inversely to price (high VIX = fear = low prices). Inverting it before scaling creates visual alignment where both VIX-line and price-line move in the same direction during bullish/bearish periods.

Amplification Feature (Optional)
Magnifies score deviations from the midpoint for easier pattern recognition:

midPrice = (minPrice + maxPrice) / 2
amplifiedValue = midPrice + (scaledValue - midPrice) * amplifyFactor
Dual Y-Axis Setup
Left axis: Price-scaled values (actual domain)
Right axis: Raw 0-100 reference scale for scores
Implementation Notes
Filter spike anomalies (>50% single-day changes) before calculating min/max
Support time period slicing (1M, 3M, 1Y, ALL)
Include zoom (Shift+wheel) and pan (drag when zoomed) interactions
Here's a prompt documenting the chart scaling methodology:

Chart Scaling System Prompt
Overview
Build a dual-axis financial chart where price is the base layer and all other metrics (scores, indicators) are visually scaled to overlay on the price chart for pattern correlation.

Core Concept
The left Y-axis domain is determined by the price range (min/max) of the asset. All non-price data is mathematically mapped onto this same domain so visual alignment reveals correlations.

Scaling Formula
scaledValue = minPrice + (value / 100) * priceRange

Where:
- minPrice = lowest price in the visible dataset
- priceRange = maxPrice - minPrice
- value = the 0-100 normalized metric (score, inverted VIX, etc.)
Data Type Handling
Data Type	Range	Scaling Method
Price	Varies	Direct plot (defines the domain)
Scores	0-100	Apply formula directly
VIX	~10-80	Invert first: 100 - vix, then apply formula
VIX Inversion Rationale
VIX moves inversely to price (high VIX = fear = low prices). Inverting it before scaling creates visual alignment where both VIX-line and price-line move in the same direction during bullish/bearish periods.

Amplification Feature (Optional)
Magnifies score deviations from the midpoint for easier pattern recognition:

midPrice = (minPrice + maxPrice) / 2
amplifiedValue = midPrice + (scaledValue - midPrice) * amplifyFactor
Dual Y-Axis Setup
Left axis: Price-scaled values (actual domain)
Right axis: Raw 0-100 reference scale for scores
Implementation Notes
Filter spike anomalies (>50% single-day changes) before calculating min/max
Support time period slicing (1M, 3M, 1Y, ALL)
Include zoom (Shift+wheel) and pan (drag when zoomed) interactions
This prompt captures the complete scaling methodology for recreating the chart system.
