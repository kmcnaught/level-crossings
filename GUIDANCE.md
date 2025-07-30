# Web Development Guidance for Level Crossing App

## Mobile-First Development
- Use `<meta name="viewport" content="width=device-width, initial-scale=1.0">` for proper mobile scaling
- Design for touch interfaces (minimum 44px touch targets)
- Test with Chrome DevTools mobile emulation
- Consider thumb-friendly UI placement

## Geolocation API Best Practices
- Always request permission explicitly with `navigator.geolocation.getCurrentPosition()`
- Provide fallback for location access denial
- Use `watchPosition()` for continuous tracking vs `getCurrentPosition()` for one-time
- Set reasonable timeout and accuracy options
- Handle location errors gracefully

## API Integration (Overpass API)
- Overpass API is CORS-enabled, safe for direct browser calls
- Use timeout parameters in queries (max 25 seconds)
- Implement exponential backoff for failed requests
- Cache responses to minimize API calls (respect fair use)
- Query format: `[out:json][timeout:10]; (node["railway"="level_crossing"](bbox)); out geom;`

## Performance Optimization
- Minimize DOM manipulations
- Use `requestAnimationFrame()` for smooth animations
- Implement lazy loading for map tiles
- Cache calculated distances to avoid repeated computation
- Use efficient data structures (Maps vs Objects for lookups)

## Leaflet.js Map Implementation
- Initialize with user's location as center
- Use `L.tileLayer()` with OpenStreetMap tiles
- Add markers with `L.marker()` and custom icons
- Implement map bounds to prevent infinite panning
- Use `L.circle()` for distance visualization

## Distance Calculations
- Haversine formula for great-circle distances
- JavaScript implementation: `Math.acos(Math.sin(lat1) * Math.sin(lat2) + Math.cos(lat1) * Math.cos(lat2) * Math.cos(lon2 - lon1)) * 6371000`
- Convert to user-friendly units (miles/kilometers)
- Use bearing calculation for direction indicators

## Error Handling
- Network failures (API unavailable)
- Geolocation denied or unavailable
- No level crossings found within radius
- Invalid API responses
- Provide user-friendly error messages

## Static Hosting Considerations
- Single HTML file with inline CSS/JS for simplicity
- No build process required
- HTTPS required for geolocation API
- Works on any static host (GitHub Pages, Netlify, etc.)

## Browser Compatibility
- Modern browsers support geolocation and fetch API
- Provide fallbacks for older browsers if needed
- Test on iOS Safari, Android Chrome
- Consider PWA manifest for app-like experience

## Security Notes
- No API keys required (Overpass API is open)
- HTTPS only for production (geolocation requirement)
- No sensitive data storage needed
- Client-side only = no server vulnerabilities