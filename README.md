# Mini Apps Collection

A collection of simple, focused web applications for everyday tasks.

## Apps

### 1. TimeFinder 🌍
**Path**: `/timefinder/`

A visual timezone comparison tool for planning meetings across multiple timezones.

**Features**:
- 24-hour timeline visualization for Sweden, Thailand, and Vietnam
- Working hours highlighted (9 AM - 5 PM)
- Current time indicator
- Toggle timezones on/off
- Mobile-friendly with synchronized scrolling
- One-click copy to clipboard

**Tech**: Pure HTML/CSS/JS, uses `Intl.DateTimeFormat` for timezone handling

### 2. VND ⇄ SEK 💱
**Path**: `/vndxsek/`

Live currency converter between Vietnamese Dong (VND) and Swedish Krona (SEK).

**Features**:
- Live exchange rate updates from exchangerate-api.com
- Instant conversion as you type (no button press needed)
- Bidirectional conversion with swap button
- Mobile-friendly design
- Works offline with fallback rates
- Auto-refreshes rates every 5 minutes

**Tech**: Pure HTML/CSS/JS, uses free exchangerate-api.com API

## Project Structure

```
/
├── index.html              # Landing page with links to all apps
├── timefinder/
│   └── index.html         # TimeFinder app
├── vndxsek/
│   └── index.html         # VND/SEK converter app
├── CLAUDE.md              # Developer documentation
└── README.md              # This file
```

## Local Development

No build process or dependencies required:

```bash
# Clone the repository
git clone https://github.com/yourusername/timefinder.git
cd timefinder

# Open in browser
open index.html

# Or use a local server
python -m http.server 8000
# Visit http://localhost:8000
```

## Deployment to GitHub Pages

1. **Enable GitHub Pages** in repository settings:
   - Go to Settings > Pages
   - Source: Deploy from a branch
   - Branch: `main`, folder: `/ (root)`
   - Save

2. **Your site will be available at**:
   ```
   https://yourusername.github.io/timefinder/
   ```

3. **Access apps**:
   - Landing page: `https://yourusername.github.io/timefinder/`
   - TimeFinder: `https://yourusername.github.io/timefinder/timefinder/`
   - VND/SEK: `https://yourusername.github.io/timefinder/vndxsek/`

## Adding New Apps

Each app should be self-contained in its own folder:

1. Create a new folder: `mkdir newapp/`
2. Add `index.html` and any assets
3. Update root `index.html` to link to the new app
4. Update this README with app description

## Browser Compatibility

All apps work on modern browsers:
- Chrome/Edge (90+)
- Firefox (88+)
- Safari (14+)
- Mobile browsers (iOS Safari, Chrome Mobile)

JavaScript must be enabled.

## License

MIT License - feel free to use and modify for your needs.
