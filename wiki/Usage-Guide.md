# Usage Guide

This guide explains how to use Commutr for route planning and business registration.

## For Commuters

### Finding a Route

#### 1. Enter Your Locations

1. Open Commutr in your browser (http://localhost:3000)
2. Click the "Source" field and enter your starting location
3. Click the "Destination" field and enter where you want to go

**Tips**:
- Use autocomplete suggestions for accurate locations
- You can also click on the map to select locations
- Addresses, landmarks, and station names all work

#### 2. Set Your Preferences

**Cost Priority**:
- Toggle "Cheapest Route" to prioritize low-cost options
- Leave off to balance cost with travel time

**Accessibility Needs**:
- **Avoid Stairs**: Filter out routes with stairs
- **Require Elevators**: Only show routes with elevator access
- **Max Walking Distance**: Set maximum walking distance in meters
- **Max Transfers**: Limit number of transfers

**Example preferences**:
```
✓ Cheapest Route
✓ Avoid Stairs
  Require Elevators
  Max Walking Distance: 500m
  Max Transfers: 2
```

#### 3. Search for Routes

Click "Find Routes" to see available options.

**What you'll see**:
- List of routes ranked by cost and accessibility
- Total fare for each route
- Travel time
- Number of transfers
- Accessibility summary

#### 4. View Route Details

Click any route to see:

**Route Overview**:
- Map visualization of the complete route
- Each transport segment color-coded by mode
- Transfer points marked clearly

**Fare Breakdown**:
```
Segment 1: Bus 42        $2.50
  Base fare:             $2.50
  Transfer fee:          $0.00
  
Segment 2: Train Red Line $3.00
  Base fare:             $2.50
  Transfer fee:          $0.50
  
Total:                   $5.50
```

**Accessibility Information**:
- Total walking distance: 450m
- Stairs: 12 steps at Station A
- Elevators: Available at all stations
- Wheelchair accessible: Yes

**Nearby Businesses**:
- Businesses within 500m of your route
- Ordered by proximity (closest first)
- Categories: cafes, restaurants, pharmacies, etc.

#### 5. Get Navigation Instructions

Click "Start Navigation" to get turn-by-turn directions:

**Text Instructions**:
```
1. Walk 200m north to Bus Stop A (3 minutes)
2. Board Bus 42 towards Downtown (15 minutes)
3. Get off at Transfer Station (12 stops)
4. Walk 150m to Train Platform B (2 minutes)
   - Take elevator to platform level
5. Board Red Line train towards Airport (20 minutes)
6. Get off at Destination Station (8 stops)
7. Walk 100m east to destination (2 minutes)
```

**Voice Instructions**:
- Click "Enable Voice" for audio guidance
- Instructions read aloud at each step
- Available in multiple languages

### Understanding Route Rankings

Routes are ranked by a combined score:

**Cost Score** (if "Cheapest Route" enabled):
- Lower fare = higher score
- Includes all fees and transfers

**Accessibility Score**:
- Fewer stairs = higher score
- Elevator availability = higher score
- Shorter walking distance = higher score
- Fewer transfers = higher score

**Final Ranking**:
- Routes meeting all your requirements appear first
- Routes violating requirements are filtered out
- Tied scores are broken by travel time

### Saving and Sharing Routes

**Save Route** (requires account):
- Click "Save Route" to add to favorites
- Access saved routes from your profile
- Set up notifications for delays

**Share Route**:
- Click "Share" to get a link
- Send link to friends or family
- Link includes all route details

### Accessibility Features

**Screen Reader Support**:
- All interface elements have proper labels
- Route information announced clearly
- Keyboard navigation fully supported

**High Contrast Mode**:
- Toggle in settings for better visibility
- Increases text and button contrast

**Text Size**:
- Adjust text size in settings
- Affects all text except maps

**Voice Navigation**:
- Turn-by-turn audio instructions
- Adjustable speech rate
- Multiple language support

## For Business Owners

### Registering Your Business

#### 1. Access Business Portal

Navigate to: http://localhost:3000/business

#### 2. Create Account

- Enter business email
- Set password
- Verify email address

#### 3. Submit Business Information

**Required Fields**:
- **Business Name**: Your official business name
- **Category**: Select from dropdown (cafe, restaurant, retail, etc.)
- **Location**: Enter address or click on map
- **Contact Info** (optional): Email and phone

**Example**:
```
Business Name: Joe's Coffee Shop
Category: Cafe
Location: 123 Main Street, Downtown
Email: joe@coffeeshop.com
Phone: (555) 123-4567
```

#### 4. Review Listing Fee

- Fixed fee: $50.00 per year
- Same price for all businesses
- No promotional upgrades available

**What you get**:
- Listing appears to commuters near your location
- Equal visibility with all other businesses
- Listing ordered by proximity only (no paid priority)

#### 5. Complete Payment

- Enter payment information
- Process listing fee
- Receive confirmation email

#### 6. Listing Activation

- Listing activates immediately after payment
- Appears to users within 500m of your location
- Visible for 1 year from activation date

### Managing Your Listing

**View Listing**:
- See how your business appears to users
- Check listing status and expiration date

**Update Information**:
- Change business name, category, or location
- Update contact information
- Changes take effect immediately

**View Metrics** (basic):
- Number of times your listing was shown
- No personal user data provided
- Updated daily

**Renew Listing**:
- Receive email reminder 30 days before expiration
- Renew online with same payment method
- Listing continues without interruption

### Understanding Business Visibility

**How Listings Appear**:
1. User searches for a route
2. System calculates optimal route
3. System finds businesses within 500m of route
4. Businesses ordered by distance (closest first)
5. All businesses shown with equal prominence

**What Affects Visibility**:
- ✅ Distance from route (closer = shown first)
- ✅ Being within 500m proximity threshold
- ❌ Payment amount (fixed fee for all)
- ❌ Listing age or renewal count
- ❌ Business size or category

**Neutrality Guarantee**:
- No sponsored positions
- No paid priority
- No promotional upgrades
- All businesses treated equally

## API Usage (For Developers)

### Authentication

Get an API key from your account settings:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
  http://localhost:3000/api/health
```

### Search for Routes

```bash
POST /api/routes/search
Content-Type: application/json

{
  "source": {
    "latitude": 40.7128,
    "longitude": -74.0060
  },
  "destination": {
    "latitude": 40.7589,
    "longitude": -73.9851
  },
  "preferences": {
    "prioritizeCost": true,
    "accessibilityRequirements": {
      "avoidStairs": true,
      "maxWalkingDistance": 500
    }
  }
}
```

**Response**:
```json
{
  "routes": [
    {
      "id": "route-123",
      "totalCost": 5.50,
      "totalDuration": 45,
      "segments": [...],
      "accessibilitySummary": {...},
      "nearbyBusinesses": [...]
    }
  ]
}
```

### Get Route Details

```bash
GET /api/routes/route-123
```

### Generate Navigation

```bash
POST /api/navigation/generate
Content-Type: application/json

{
  "routeId": "route-123",
  "format": "text"  // or "voice"
}
```

See full API documentation at: http://localhost:3000/api/docs

## Troubleshooting

### No Routes Found

**Possible causes**:
- Locations too far apart
- No public transport between locations
- Accessibility requirements too strict

**Solutions**:
- Check locations are correct
- Relax accessibility requirements
- Try nearby alternative locations

### Route Calculation Slow

**Possible causes**:
- Complex route with many transfers
- First-time calculation (not cached)
- High server load

**Solutions**:
- Wait a few seconds (usually < 5s)
- Refresh page if stuck
- Try again during off-peak hours

### Business Not Appearing

**Possible causes**:
- Business more than 500m from route
- Listing expired
- Payment not processed

**Solutions**:
- Check listing status in business portal
- Verify payment was successful
- Ensure location is correct

### Voice Navigation Not Working

**Possible causes**:
- Browser doesn't support Web Speech API
- Microphone permissions not granted
- Audio output disabled

**Solutions**:
- Use Chrome, Edge, or Safari
- Grant microphone permissions
- Check system audio settings

## Tips and Best Practices

### For Better Route Results

1. **Be Specific**: Use exact addresses rather than general areas
2. **Check Timing**: Some routes only available at certain times
3. **Consider Alternatives**: Try nearby stations if no direct route
4. **Save Favorites**: Save frequently used routes for quick access

### For Business Owners

1. **Accurate Location**: Ensure your location pin is exactly correct
2. **Complete Profile**: Fill in all optional fields for better presentation
3. **Renew Early**: Don't wait until expiration to renew
4. **Monitor Metrics**: Check views regularly to understand visibility

### Accessibility Tips

1. **Test Routes**: Do a test run before important trips
2. **Allow Extra Time**: Accessible routes may take longer
3. **Report Issues**: Let us know if accessibility info is wrong
4. **Use Voice**: Voice navigation helps when hands are full

## Getting Help

**In-App Help**:
- Click "?" icon for contextual help
- Hover over fields for tooltips
- Check FAQ section

**Community Support**:
- GitHub Discussions for questions
- GitHub Issues for bug reports
- Email support (if configured)

**Documentation**:
- [System Architecture](System-Architecture) for technical details
- [FAQ](FAQ) for common questions
- API docs for developers

---

*Questions not answered here? Check the [FAQ](FAQ) or ask in GitHub Discussions.*
