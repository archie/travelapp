# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**TimeFinder** is a single-page web application for visualizing meeting times between Vietnam (Asia/Ho_Chi_Minh) and Sweden (Europe/Stockholm) timezones. Built as a pure static HTML/CSS/JavaScript application optimized for GitHub Pages hosting.

## Development Commands

### Testing Locally

```bash
# Open directly in browser
open index.html

# Or serve locally (recommended for testing)
python -m http.server 8000
# Then visit http://localhost:8000
```

### Deployment

```bash
# Commit and push to main branch
git add .
git commit -m "Update timezone visualizer"
git push origin main

# GitHub Pages will automatically deploy from main branch
```

## Architecture

### Single-File Application (index.html)

The entire application is self-contained in `index.html` with:
- **Embedded CSS**: All styles in `<style>` tag (no external stylesheets)
- **Embedded JavaScript**: Complete functionality in `<script>` tag (no external JS files)
- **No build process**: Direct deployment to GitHub Pages
- **No dependencies**: Pure vanilla JavaScript, no frameworks or libraries

### JavaScript Architecture

**TimeFinder Class** (`index.html:line ~230`):
- Main application controller
- Manages state and coordinates UI updates
- Handles timezone conversions using `Intl.DateTimeFormat` API

**Key Methods**:
- `init()`: Initializes app, sets default to current Vietnam time
- `getTimeInZone(hour, timezone)`: Converts selected Vietnam hour to target timezone
- `renderTimelines()`: Generates 24-hour timeline HTML for both zones
- `selectHour(hour)`: Updates selected time and refreshes display
- `copyToClipboard()`: Copies formatted meeting time with fallback for older browsers

### Timezone Handling

Uses browser's native `Intl.DateTimeFormat` API:
- **Vietnam**: `Asia/Ho_Chi_Minh` (UTC+7, no DST)
- **Sweden**: `Europe/Stockholm` (UTC+1/+2 with automatic DST handling)
- **Conversion**: Create Date in Vietnam time, convert to target timezone
- **DST**: Browser automatically handles daylight saving transitions

### CSS Design System

**CSS Variables** (`index.html:line ~9`):
- `--primary-color`: Main brand color
- `--working-hours`: Light blue background for 9 AM - 5 PM
- `--selected-time`: Highlight color for selected hour
- `--current-time`: Yellow outline for current hour

**Layout**:
- CSS Grid for 24-hour timeline (24 equal columns)
- Flexbox for time display and responsive stacking
- Mobile-first responsive design with breakpoints at 768px and 480px

## Key Features Implementation

### Timeline Visualization
- Each hour is a clickable block in a 24-column grid
- Working hours (9-17) have blue background
- Night hours (22-6) have gray background
- Current hour marked with yellow outline
- Selected hour highlighted in dark blue

### Time Selection & Sync
- Clicking any hour in Vietnam timeline updates both displays
- Sweden timeline shows corresponding time (accounting for DST)
- Both timelines highlight the same selected "moment in time"

### Copy to Clipboard
- Primary: Uses modern `navigator.clipboard.writeText()` API
- Fallback: Uses `document.execCommand('copy')` for older browsers
- Visual feedback: Button changes to "Copied!" with green background

## Testing Considerations

### Manual Testing Checklist
1. **Timezone accuracy**: Verify times match actual Vietnam/Sweden times
2. **DST transitions**: Test around March/October when Sweden changes time
3. **Day crossover**: Select late evening hours to verify day changes correctly
4. **Mobile responsiveness**: Test on phone screens (horizontal scroll for timeline)
5. **Clipboard**: Test copy functionality on different browsers
6. **Touch interactions**: Verify hour selection works on touch devices

### Edge Cases
- **Midnight crossings**: Times near midnight may show different days
- **DST transitions**: Hour may not exist or repeat during DST changes
- **Time difference**: Vietnam/Sweden offset varies (5-6 hours) based on DST

## Modification Guidelines

### Changing Timezones
To adapt for different timezone pairs, modify:
- `this.vietnamTZ` and `this.swedenTZ` in constructor
- Update UI labels in HTML (timeline headers and time display)
- Adjust `calculateTimeDifference()` method if needed

### Styling Changes
- Modify CSS variables in `:root` for consistent theming
- Working hours range: Change `isWorkingHour()` method and update legend
- Timeline layout: Adjust `grid-template-columns` in `.timeline` class

### Adding Features
Keep the single-file architecture:
- Add new JavaScript code within existing `<script>` tag
- Add new CSS within existing `<style>` tag
- Maintain mobile-first responsive approach

## File Structure

```
/
├── index.html    # Complete application (HTML/CSS/JS)
├── README.md     # User documentation
└── CLAUDE.md     # This file (developer documentation)
```

## Performance Notes

- Total file size: ~18KB (uncompressed)
- No external requests (no CDNs, no fonts)
- Loads instantly on GitHub Pages
- No JavaScript bundling or minification needed
