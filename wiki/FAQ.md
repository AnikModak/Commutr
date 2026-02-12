# Frequently Asked Questions

## General Questions

### What is Commutr?

Commutr is an open-source platform that helps commuters find the cheapest and most accessible public transport routes. It also provides fair visibility to local businesses along routes without promotional bias.

### Who is Commutr for?

**Commuters**: Anyone using public transport who wants to save money and navigate accessible routes.

**Business Owners**: Local shopkeepers seeking fair visibility along popular commuter routes.

**Developers**: Contributors interested in public transport, accessibility, or ethical business models.

### Is Commutr free to use?

Yes, Commutr is free for commuters. Business owners pay a fixed annual listing fee ($50) for visibility, but this doesn't affect how routes are calculated or how businesses are displayed.

### Which cities does Commutr support?

Currently, Commutr is being developed for a single city. Multi-city support is planned for 2027. See the [Roadmap](Roadmap) for details.

### Is Commutr open source?

Yes, Commutr is released under the MIT License. You can view, modify, and contribute to the code on GitHub.

## Using Commutr

### How do I find a route?

1. Enter your source and destination
2. Set your preferences (cost priority, accessibility needs)
3. Click "Find Routes"
4. View ranked route options
5. Select a route for detailed navigation

See the [Usage Guide](Usage-Guide) for detailed instructions.

### Why are some routes not showing up?

Possible reasons:
- Routes don't meet your accessibility requirements
- No public transport available between locations
- Locations are outside the service area
- Transport data is incomplete

Try relaxing your accessibility requirements or checking nearby alternative locations.

### How are routes ranked?

Routes are ranked by a combined score:
- **Cost**: Lower fare = higher score (if "Cheapest Route" enabled)
- **Accessibility**: Fewer stairs, shorter walking distance, more elevators = higher score
- **Time**: Faster routes break ties

Routes that don't meet your requirements are filtered out entirely.

### Can I save routes for later?

Not yet. User accounts and saved routes are planned for Q3 2026. See the [Roadmap](Roadmap).

### Does Commutr work offline?

Not currently. Offline support is planned for mobile apps in 2027.

### How accurate is the fare information?

Fare data comes from official transport authority APIs. We update it regularly, but prices may change. Always verify fares with your local transport provider.

### How accurate is the accessibility information?

We source accessibility data from transport authorities and validate it where possible. However, some data may be incomplete or outdated. If you find errors, please report them so we can improve.

## Accessibility

### What accessibility features does Commutr support?

- **Avoid Stairs**: Filter out routes with stairs
- **Require Elevators**: Only show routes with elevator access
- **Max Walking Distance**: Set maximum walking distance
- **Max Transfers**: Limit number of transfers
- **Screen Reader Support**: Full keyboard navigation and ARIA labels
- **Voice Navigation**: Audio turn-by-turn instructions

### Can I report incorrect accessibility information?

Yes! Please open an issue on GitHub with:
- Location/station name
- What's incorrect
- Correct information (if known)
- Photos (if possible)

### Is Commutr WCAG compliant?

We strive for WCAG 2.1 AA compliance. If you find accessibility issues, please report them.

### Does voice navigation work in all browsers?

Voice navigation uses the Web Speech API, which works in:
- Chrome/Edge (full support)
- Safari (partial support)
- Firefox (limited support)

For best results, use Chrome or Edge.

## For Business Owners

### How do I register my business?

1. Go to the business portal
2. Create an account
3. Submit business information
4. Pay the listing fee ($50/year)
5. Your listing activates immediately

See the [Usage Guide](Usage-Guide) for detailed steps.

### How much does it cost?

$50 per year, fixed for all businesses. No promotional upgrades or paid priority.

### How will my business be displayed?

Your business appears to users whose routes pass within 500 meters of your location. Businesses are ordered by proximity only—closest first. All businesses have equal visual prominence.

### Can I pay more for better placement?

No. Commutr doesn't offer paid priority or promotional upgrades. All businesses are treated equally regardless of payment amount. This is a core principle of the platform.

### What if my business doesn't appear?

Check:
- Is your listing active? (Check business portal)
- Is payment processed?
- Is your location correct?
- Are routes passing within 500m of your location?

If everything looks correct but you're still not appearing, contact support.

### Can I update my business information?

Yes, you can update your business name, category, location, and contact info anytime through the business portal. Changes take effect immediately.

### What happens when my listing expires?

You'll receive an email reminder 30 days before expiration. If not renewed, your listing deactivates and stops appearing to users. You can renew anytime to reactivate.

### Can I see how many people viewed my listing?

Yes, basic metrics are available in the business portal:
- Number of times your listing was shown
- Updated daily

We don't provide personal user data or detailed analytics.

## Technical Questions

### What technologies does Commutr use?

**Frontend**: React, TypeScript, Tailwind CSS, Mapbox  
**Backend**: Node.js, Express.js, Python, FastAPI  
**Database**: PostgreSQL, PostGIS, Redis  
**Cloud**: AWS (EC2, RDS, S3, CloudFront)

See [Tech Stack & Tools](Tech-Stack-&-Tools) for detailed explanations.

### Why TypeScript instead of JavaScript?

TypeScript catches errors at compile time, makes refactoring safer, and improves code documentation through type definitions. This is especially important for a project with multiple contributors.

### Why PostgreSQL instead of MongoDB?

We need strong consistency guarantees for business listings and route data. PostgreSQL's ACID compliance and PostGIS spatial features are better suited to our needs than MongoDB's eventual consistency model.

### Why not use serverless (AWS Lambda)?

Route calculation can take several seconds for complex queries. Lambda's timeout limits and cold start latency don't fit our use case well. Traditional servers give us more control.

### How do you handle real-time transport data?

Currently, we don't. Real-time updates are planned for Q4 2026. We'll integrate with transport authority APIs that provide live delay information.

### Is there an API?

Yes, a REST API is available for developers. See the [Usage Guide](Usage-Guide) for API documentation.

## Design Decisions

### Why not show ads?

Ads compromise our mission of transparency and fairness. We believe users deserve unbiased route information without commercial influence.

### Why charge businesses at all?

The listing fee covers infrastructure costs and prevents spam. The fixed fee (same for all businesses) ensures fairness while keeping the platform sustainable.

### Why not integrate ride-sharing (Uber, Lyft)?

Commutr focuses exclusively on public transport. Ride-sharing services have different pricing models and don't align with our accessibility-first, cost-transparent philosophy.

### Why not add social features?

We may add limited community features (route reviews) in the future, but Commutr is not a social network. We want to stay focused on route planning.

### Why open source?

Open source ensures transparency, enables community contributions, and aligns with our values of fairness and accessibility. Anyone can verify that business listings are truly neutral.

## Contributing

### How can I contribute?

Many ways:
- Report bugs
- Suggest features
- Write code
- Improve documentation
- Review pull requests
- Answer questions
- Spread the word

See the [Contribution Guide](Contribution-Guide) for details.

### I'm new to open source. Where do I start?

Look for issues labeled `good first issue`. These are well-defined, beginner-friendly tasks with guidance provided. The [Contribution Guide](Contribution-Guide) has a section specifically for first-time contributors.

### Do I need to know TypeScript?

Not necessarily. You can contribute by:
- Improving documentation
- Writing tests
- Reporting bugs
- Suggesting features
- Reviewing pull requests

If you want to write code, TypeScript knowledge helps, but we're happy to help you learn.

### How long does it take for pull requests to be reviewed?

Usually 2-3 days. Maintainers are volunteers with limited time, so please be patient. If your PR hasn't been reviewed after a week, feel free to ping us.

### Can I work on multiple issues at once?

It's better to focus on one issue at a time. This prevents conflicts and ensures quality. Once your first PR is merged, feel free to pick up another issue.

## Performance

### Why is route calculation slow?

Complex routes with many transfers can take 3-5 seconds to calculate. First-time calculations aren't cached. We're working on performance improvements—see the [Roadmap](Roadmap).

### How can I make it faster?

- Use cached routes when possible
- Simplify accessibility requirements
- Try nearby alternative locations
- Wait for performance improvements (Q3 2026)

### What's the maximum number of routes I can compare?

Currently, we return up to 5 routes. This balances comprehensiveness with performance. More routes would slow down calculation significantly.

### Does Commutr work on slow connections?

The initial load requires downloading map data and assets. Once loaded, route searches are relatively lightweight. Offline support is planned for mobile apps.

## Privacy & Security

### What data does Commutr collect?

**For commuters** (no account):
- Search queries (source, destination, preferences)
- Anonymized usage statistics
- No personal information

**For business owners**:
- Business information (name, location, category)
- Contact information (email, phone)
- Payment information (handled by payment processor, not stored by us)

### Is my data shared with third parties?

No. We don't sell or share user data. Transport APIs may log requests, but we don't provide them with personal information.

### How is payment information secured?

Payment processing is handled by a PCI-compliant payment processor. We never store credit card information on our servers.

### Can I delete my data?

Yes. Business owners can delete their accounts and all associated data through the business portal. For commuters (once accounts are added), account deletion will be available in settings.

## Troubleshooting

### The map isn't loading

Check:
- Is your internet connection working?
- Is JavaScript enabled?
- Are you using a supported browser? (Chrome, Firefox, Safari, Edge)
- Check browser console for errors

### I'm getting a 500 error

This is a server error. Please:
1. Try again in a few minutes
2. If it persists, report it on GitHub with:
   - What you were trying to do
   - Browser and OS
   - Screenshot of error (if visible)

### Voice navigation isn't working

Check:
- Are you using Chrome, Edge, or Safari?
- Have you granted microphone permissions?
- Is audio output enabled?
- Try refreshing the page

### My question isn't answered here

- Search [GitHub Discussions](https://github.com/YOUR_USERNAME/commutr/discussions)
- Check other Wiki pages
- Open a new discussion if your question isn't answered

---

*Have a question not listed here? Ask in [GitHub Discussions](https://github.com/YOUR_USERNAME/commutr/discussions) and we'll add it to this FAQ.*
