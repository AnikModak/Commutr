# Roadmap

This page outlines Commutr's current status, planned features, and long-term vision.

## Current Status

**Version**: 0.1.0 (Alpha)  
**Status**: Active Development  
**Last Updated**: February 2026

### What's Working

✅ **Core Route Planning**
- Find routes between two locations
- Calculate optimal paths using public transport
- Support for buses, trains, subways, trams

✅ **Fare Calculation**
- Compute total fare for routes
- Break down costs by segment
- Include transfer fees and zone charges

✅ **Basic UI**
- Location input with autocomplete
- Route visualization on map
- List view of route options

✅ **Database Infrastructure**
- PostgreSQL with PostGIS
- Redis caching
- Data persistence

### In Progress

🚧 **Accessibility Analysis** (80% complete)
- Evaluate stairs, elevators, walking distances
- Filter routes by accessibility requirements
- Display accessibility summaries
- **ETA**: March 2026

🚧 **Business Registration** (60% complete)
- Business owner portal
- Registration form and validation
- Payment processing integration
- **ETA**: April 2026

🚧 **Navigation Instructions** (40% complete)
- Step-by-step text instructions
- Voice navigation support
- **ETA**: May 2026

### Not Started

❌ Mobile applications
❌ Real-time updates
❌ User accounts and saved routes
❌ Multi-language support
❌ Crowdsourced data

## Short-Term Goals (Next 6 Months)

### Q1 2026 (Jan-Mar)

**Focus**: Complete Core Features

- [x] Set up project infrastructure
- [x] Implement route planning algorithm
- [x] Build fare calculator
- [ ] **Complete accessibility analyzer** (March)
- [ ] Add comprehensive test coverage
- [ ] Deploy to staging environment

**Success Metrics**:
- All core features functional
- 80%+ test coverage
- < 2 second route calculation time

### Q2 2026 (Apr-Jun)

**Focus**: Business Features & Polish

- [ ] **Complete business registration** (April)
- [ ] Implement proximity-based business search
- [ ] Add navigation instructions (May)
- [ ] Improve UI/UX based on feedback
- [ ] Launch closed beta (June)

**Success Metrics**:
- 10 businesses registered
- 100 beta users onboarded
- Positive feedback on usability

## Mid-Term Goals (6-12 Months)

### Q3 2026 (Jul-Sep)

**Focus**: Scale & Reliability

**Features**:
- User accounts and authentication
- Save favorite routes
- Route history
- Email notifications for delays
- Performance optimizations

**Infrastructure**:
- Production deployment on AWS
- Monitoring and alerting
- Automated backups
- Load testing

**Success Metrics**:
- 1,000 active users
- 99.9% uptime
- < 1 second cached route response

### Q4 2026 (Oct-Dec)

**Focus**: Mobile & Real-Time

**Features**:
- Mobile-responsive web design
- Real-time delay notifications
- Dynamic route recalculation
- Push notifications
- Offline route caching

**Data Quality**:
- Integrate with more transport APIs
- Validate and clean accessibility data
- Add crowdsourced updates

**Success Metrics**:
- 50% mobile traffic
- Real-time updates within 5 minutes
- 90% data accuracy

## Long-Term Vision (1-3 Years)

### 2027: Expansion

**Multi-City Support**:
- Expand beyond initial city
- Support 5-10 major cities
- Handle different transport systems
- Multi-currency support

**Native Mobile Apps**:
- iOS app (Swift/SwiftUI)
- Android app (Kotlin)
- Offline functionality
- Background location tracking

**Advanced Features**:
- Route sharing with friends
- Group trip planning
- Calendar integration
- Weather-aware routing

### 2028: Community

**User-Generated Content**:
- Route reviews and ratings
- Accessibility feedback from users
- Photo uploads of stations
- Report issues (broken elevators, etc.)

**Social Features**:
- Follow frequent routes
- See popular routes
- Community tips and tricks
- Local transport news

**Gamification**:
- Badges for eco-friendly travel
- Challenges and achievements
- Leaderboards for sustainable commuting

### 2029: Intelligence

**AI Enhancements**:
- Predict delays before they're announced
- Personalized route recommendations
- Learn user preferences over time
- Natural language queries

**Sustainability**:
- Carbon footprint tracking
- Compare environmental impact
- Incentives for green travel
- Partner with environmental organizations

**Accessibility Innovation**:
- AR navigation for visually impaired
- Real-time crowdsourced accessibility updates
- Predictive accessibility (elevator outages)
- Partnership with accessibility advocates

## Known Limitations

### Current Limitations

**Geographic Coverage**:
- Limited to single city initially
- Requires local transport API access
- May not cover all transport modes

**Data Quality**:
- Accessibility data may be incomplete
- Real-time updates not yet available
- Some routes may be missing

**Performance**:
- Complex routes may take 3-5 seconds
- First-time calculations not cached
- Limited concurrent user capacity

**Features**:
- No user accounts yet
- No mobile apps
- No real-time updates
- English only

### Technical Debt

**Code Quality**:
- Some components need refactoring
- Test coverage gaps in older code
- Documentation incomplete in places

**Infrastructure**:
- Single server (no redundancy yet)
- Manual deployment process
- Limited monitoring

**Data**:
- No automated data validation
- Manual data updates required
- No data versioning

## Areas Where Contributors Are Welcome

### High Priority

🔥 **Accessibility Analysis**
- Implement remaining accessibility features
- Add property-based tests
- Validate against real-world data
- **Skills needed**: TypeScript, algorithms, testing

🔥 **Business Registration**
- Complete payment integration
- Build business owner dashboard
- Add listing management features
- **Skills needed**: TypeScript, React, payment APIs

🔥 **Documentation**
- Improve setup guides
- Add API documentation
- Create video tutorials
- **Skills needed**: Technical writing, video editing

### Medium Priority

⚡ **Testing**
- Increase test coverage
- Add more property-based tests
- Create end-to-end tests
- **Skills needed**: Jest, fast-check, testing best practices

⚡ **UI/UX Improvements**
- Improve mobile responsiveness
- Add loading states
- Better error messages
- **Skills needed**: React, CSS, UX design

⚡ **Performance**
- Optimize route algorithms
- Improve caching strategy
- Database query optimization
- **Skills needed**: Algorithms, PostgreSQL, Redis

### Future Work

💡 **Mobile Apps**
- iOS app development
- Android app development
- **Skills needed**: Swift/Kotlin, mobile development

💡 **Real-Time Features**
- WebSocket implementation
- Real-time delay tracking
- **Skills needed**: WebSockets, real-time systems

💡 **Multi-Language Support**
- Internationalization (i18n)
- Translation management
- **Skills needed**: i18n, translation

## How to Influence the Roadmap

### Suggest Features

1. Check if feature is already planned (this page)
2. Search existing feature requests
3. Open new feature request with use cases
4. Participate in discussions

### Vote on Features

- 👍 React to feature requests you want
- Comment with your use case
- Help refine the proposal

### Contribute Code

- Pick an item from "Areas Where Contributors Are Welcome"
- Comment on the issue to claim it
- Submit a pull request

### Sponsor Development

- Sponsor specific features
- Fund infrastructure costs
- Support maintainer time

## Release Schedule

### Versioning

We follow [Semantic Versioning](https://semver.org/):
- **Major** (1.0.0): Breaking changes
- **Minor** (0.1.0): New features, backwards compatible
- **Patch** (0.0.1): Bug fixes

### Release Cadence

**Alpha** (current):
- Releases as features complete
- Breaking changes allowed
- Limited user base

**Beta** (Q2 2026):
- Monthly releases
- Feature freeze periods
- Wider user testing

**Stable** (Q4 2026):
- Quarterly major/minor releases
- Patch releases as needed
- Stable API

## Milestones

### Milestone 1: Core Features Complete ✅
- Route planning ✅
- Fare calculation ✅
- Basic UI ✅
- **Completed**: January 2026

### Milestone 2: Accessibility & Business 🚧
- Accessibility analysis (in progress)
- Business registration (in progress)
- Navigation instructions (in progress)
- **Target**: May 2026

### Milestone 3: Beta Launch 📅
- User accounts
- Saved routes
- Mobile responsive
- **Target**: June 2026

### Milestone 4: Production Ready 📅
- Performance optimized
- Monitoring in place
- Documentation complete
- **Target**: September 2026

### Milestone 5: Mobile Apps 📅
- iOS app
- Android app
- Offline support
- **Target**: Q2 2027

## Success Metrics

### User Metrics

**Current**:
- Active users: ~10 (internal testing)
- Routes calculated: ~500
- Businesses registered: 0

**6 Month Targets**:
- Active users: 1,000
- Routes calculated: 10,000/month
- Businesses registered: 50

**1 Year Targets**:
- Active users: 10,000
- Routes calculated: 100,000/month
- Businesses registered: 500

### Technical Metrics

**Current**:
- Test coverage: 65%
- Route calculation: 2-3 seconds
- Uptime: 95% (dev environment)

**6 Month Targets**:
- Test coverage: 80%
- Route calculation: < 2 seconds
- Uptime: 99.5%

**1 Year Targets**:
- Test coverage: 90%
- Route calculation: < 1 second (cached)
- Uptime: 99.9%

### Impact Metrics

**Goals**:
- Money saved by users through cost optimization
- Accessible routes successfully navigated
- Small businesses gaining visibility
- Carbon emissions reduced through public transport use

## Staying Updated

### Follow Progress

- **GitHub**: Watch repository for updates
- **Releases**: Subscribe to release notifications
- **Discussions**: Join community discussions
- **Blog**: Read development updates (if available)

### Provide Feedback

- **Surveys**: Participate in user surveys
- **Beta Testing**: Join beta program
- **Feature Requests**: Suggest improvements
- **Bug Reports**: Report issues

---

*This roadmap is a living document and will evolve based on user feedback, technical constraints, and community contributions. Last updated: February 2026*
