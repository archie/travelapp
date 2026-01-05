# TimeFinder

A visual timezone comparison tool for planning meetings between Vietnam and Sweden.

## Features

- **24-Hour Timeline Visualization**: See both timezones side-by-side with interactive hour blocks
- **Working Hours Highlighted**: Easily identify 9 AM - 5 PM business hours in both zones
- **Current Time Indicator**: Automatically shows the current hour in both timezones
- **Day of Week Display**: See which day it is in each timezone (important for times that cross midnight)
- **One-Click Copy**: Copy meeting times to clipboard with a single click
- **Mobile Friendly**: Fully responsive design works on phones, tablets, and desktops
- **No Installation Required**: Pure HTML/CSS/JS - just open and use

## Usage

1. **Open the app**: Visit the hosted page or open `index.html` in your browser
2. **View current time**: The app defaults to the current time in Vietnam
3. **Select a time**: Click any hour block on either timeline to select a meeting time
4. **Check both zones**: The selected time updates automatically in both timezones
5. **Copy time**: Click the "Copy Meeting Time" button to copy the formatted meeting time

### Understanding the Timeline

- **Blue blocks**: Working hours (9 AM - 5 PM)
- **Yellow outline**: Current time
- **Dark blue (selected)**: Your selected meeting time
- **Gray blocks**: Night hours (10 PM - 6 AM)

### Time Zones

- **Vietnam**: Asia/Ho_Chi_Minh (UTC+7) - No daylight saving time
- **Sweden**: Europe/Stockholm (UTC+1 in winter, UTC+2 in summer) - Automatically handles DST

## Local Development

No build process or dependencies required. Simply:

```bash
# Clone the repository
git clone https://github.com/yourusername/timefinder.git

# Open in browser
open index.html
# or on Linux: xdg-open index.html
# or on Windows: start index.html
```

You can also use a local server for development:

```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js (if you have http-server installed)
npx http-server
```

Then visit `http://localhost:8000` in your browser.

## Deployment to GitHub Pages

1. **Enable GitHub Pages** in your repository settings:
   - Go to Settings > Pages
   - Source: Deploy from a branch
   - Branch: `main` (or `master`), folder: `/ (root)`
   - Save

2. **Your site will be available at**:
   ```
   https://yourusername.github.io/timefinder/
   ```

3. **Updates**: Any changes pushed to the main branch will automatically update the site

## Browser Compatibility

Works on all modern browsers:
- Chrome/Edge (90+)
- Firefox (88+)
- Safari (14+)
- Mobile browsers (iOS Safari, Chrome Mobile)

Requires JavaScript enabled.

## Technical Details

- **Pure static files**: No frameworks, no build process
- **Timezone handling**: Uses browser's native `Intl.DateTimeFormat` API
- **DST aware**: Automatically handles daylight saving time transitions
- **Performance**: Lightweight (<50KB total)
- **Accessibility**: Semantic HTML and keyboard navigation support

## License

MIT License - feel free to use and modify for your needs.
