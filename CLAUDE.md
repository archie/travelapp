# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Mini Apps Collection** - A repository containing multiple simple, focused web applications, each in its own folder. All apps are pure static HTML/CSS/JavaScript with no build process, optimized for GitHub Pages hosting.

## Repository Structure

```
/
├── index.html              # Landing page with links to all apps
├── timefinder/
│   └── index.html         # TimeFinder timezone comparison app
├── vndxsek/
│   └── index.html         # VND/SEK currency converter
├── CLAUDE.md              # This file (developer documentation)
└── README.md              # User documentation
```

## Development Commands

### Testing Locally

```bash
# Open landing page
open index.html

# Or serve locally (recommended)
python -m http.server 8000
# Visit http://localhost:8000
```

### Deployment

```bash
# Commit and push to main branch
git add .
git commit -m "Update apps"
git push origin main

# GitHub Pages will automatically deploy from main branch
```

### Adding New Apps

```bash
# Create new app folder
mkdir newapp/

# Create app
# Add newapp/index.html with self-contained app

# Update root index.html to link to new app
# Update README.md with app description
```

## Apps Architecture

### 1. TimeFinder (`/timefinder/`)

**Purpose**: Visual timezone comparison for Sweden, Thailand, and Vietnam

**Key Features**:
- 24-hour vertical timeline visualization
- Three timezones with toggle controls
- Working hours highlighted (9 AM - 5 PM)
- Synchronized scrolling on mobile
- Vietnam as default reference timezone

**Tech Stack**:
- Single HTML file with embedded CSS/JS
- Uses `Intl.DateTimeFormat` for timezone handling
- No external dependencies

**Key Implementation Details**:
- `TimeFinder` class manages state and UI
- Timezones: `{ sweden: 'Europe/Stockholm', thailand: 'Asia/Bangkok', vietnam: 'Asia/Ho_Chi_Minh' }`
- Dynamic grid layout adjusts to visible columns
- Mobile: Vertical timelines, desktop: Can be horizontal or vertical based on screen

### 2. VND/SEK Converter (`/vndxsek/`)

**Purpose**: Live currency conversion between Vietnamese Dong and Swedish Krona

**Key Features**:
- Live exchange rates from exchangerate-api.com
- Instant conversion as user types (no button needed)
- **1000× multiplier for VND input** (user enters thousands, app converts actual amount)
- Bidirectional conversion with swap button
- Auto-refresh every 5 minutes
- Fallback rates for offline use
- Compact mobile design optimized for keyboard visibility

**Tech Stack**:
- Single HTML file with embedded CSS/JS
- Uses exchangerate-api.com free API (1,500 requests/month)
- No external dependencies

**Key Implementation Details**:
- `CurrencyConverter` class manages state and API calls
- API: `https://api.exchangerate-api.com/v4/latest/{currency}`
- **VND Input Multiplier**: When converting FROM VND, input is multiplied by 1,000
  - Example: User enters `100` → Converts `100,000 VND`
  - Hint displayed: "Enter amount in thousands (×1,000)"
  - Hint auto-hides when converting FROM SEK
- VND formatted without decimals, SEK with 2 decimals
- Swap functionality reverses conversion direction and updates hint visibility

**Mobile Optimizations**:
- Compact layout on ≤640px screens to keep both input and result above keyboard
- Reduced padding, margins, and font sizes
- Body aligned to `flex-start` instead of `center`
- Result display: min-height 60px (vs 80px desktop)
- All vertical spacing reduced by ~30-40% on mobile

**API Notes**:
- Free tier requires no API key
- Rate limits: 1,500 requests/month
- Fallback: Hardcoded approximate rates if API fails

## Common Patterns

### Single-File Apps
All apps follow the same pattern:
- Complete application in one `index.html` file
- Embedded `<style>` tag for all CSS
- Embedded `<script>` tag for all JavaScript
- No build process, no external dependencies
- Mobile-first responsive design
- **Back navigation**: Each app includes `<a href="../" class="back-link">← Back to Apps</a>` at the top

### Styling
- CSS variables in `:root` for consistent theming
- Mobile breakpoints at 768px (tablet) and 640px or 480px (phone)
- Gradient backgrounds: `linear-gradient(135deg, #667eea 0%, #764ba2 100%)`
- White content cards with rounded corners
- Back link styling:
  ```css
  .back-link {
      display: inline-block;
      color: var(--text-secondary);
      text-decoration: none;
      font-size: 0.9rem;
      margin-bottom: 1rem;
      transition: color 0.2s;
  }
  .back-link:hover {
      color: var(--primary-color);
  }
  ```

### JavaScript
- ES6 class-based architecture
- Event-driven updates
- Uses modern browser APIs (`Intl`, `fetch`, `navigator.clipboard`)
- Fallbacks for older browsers where needed

## Testing Considerations

### TimeFinder
1. Verify timezone accuracy against actual times
2. Test DST transitions (March/October for Sweden)
3. Test day crossover for evening times
4. Verify synchronized scrolling on mobile
5. Test toggle functionality with different combinations

### VND/SEK Converter
1. Verify exchange rate accuracy
2. Test offline fallback
3. Test swap functionality
4. Verify number formatting (VND no decimals, SEK 2 decimals)
5. Test live updates on input change
6. **Test 1000× multiplier**: Enter `100` VND → should convert `100,000 VND`
7. **Test hint visibility**: Hint shows for VND→SEK, hides for SEK→VND
8. **Test mobile keyboard**: On phone, verify both input and result visible when keyboard is open
9. Test compact mobile layout maintains usability

## Modification Guidelines

### Adding New Apps
1. Create folder: `mkdir newapp/`
2. Create self-contained `index.html`
3. Follow existing patterns (single file, embedded styles/scripts)
4. Add back link to root: `<a href="../">← Back to Apps</a>`
5. Update root `index.html` with new app card
6. Update `README.md` with app description

### Modifying Existing Apps
- Keep single-file architecture
- Maintain mobile-first responsive design
- Use CSS variables for theming consistency
- Add fallbacks for critical features
- Test on mobile and desktop
- **Mobile keyboard considerations**: Ensure critical UI elements remain visible above keyboard on mobile
  - Use compact layouts on small screens (≤640px)
  - Align body to `flex-start` instead of `center` on mobile
  - Test with on-screen keyboard open
  - Reduce vertical spacing as needed

### Styling Consistency
- Use shared color palette across apps
- Maintain similar card/button styles
- Keep consistent spacing and typography
- Use same gradient backgrounds

## Performance Notes

- All apps load instantly (< 50KB each)
- No external requests except for APIs (VND/SEK converter)
- No JavaScript bundling needed
- No CSS preprocessing needed
- Perfect Lighthouse scores possible
