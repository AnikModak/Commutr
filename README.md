# 🚍 Commutr - Smart Public Transport Helper

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs not-accepting](https://img.shields.io/badge/PRs-not%20accepting-red.svg)](http://makeapullrequest.com)

> An AI-powered platform that helps commuters find the cheapest and most accessible public transport routes while providing neutral visibility to local businesses.

## 🌟 Overview

Commutr is a web-based platform designed to solve two key challenges:
1. **For Commuters**: Finding optimal public transport routes based on cost and accessibility needs
2. **For Local Businesses**: Gaining fair visibility along popular routes without promotional bias

### Key Features

✅ **Cost-Optimized Routing** - Find the cheapest public transport combinations  
✅ **Accessibility-First Design** - Complete information on stairs, walking distances, and transfers  
✅ **Step-by-Step Navigation** - Text and voice-based turn-by-turn instructions  
✅ **Neutral Business Discovery** - Local businesses displayed by proximity only, no paid promotions  
✅ **Transparent Fare Breakdown** - Detailed cost analysis for every route segment  

## 📊 System Architecture

![System Architecture](.kiro/specs/commutr/system-architecture.jpg)

The platform follows a modular architecture with clear separation of concerns:

- **Web Client**: Browser-based UI for user input and route display
- **API Layer**: Request handling, authentication, and validation
- **Core Services**: Route discovery, fare optimization, and accessibility analysis
- **Processing Layer**: Ranking engine and response formatting
- **Data Layer**: Transport data store and business listings

## 🔄 Process Flow

![Process Flow](.kiro/specs/commutr/detailed-process-flow.jpg)

The user journey follows a simple, intuitive flow:
1. User enters source and destination
2. Selects preferences (cost priority, accessibility needs)
3. System validates and fetches available routes
4. Calculates fares and checks accessibility
5. Ranks routes by cost and accessibility score
6. Delivers optimized route with nearby businesses

## 🎯 Core Principles

### 1. **Neutrality**
Business listings are **never** prioritized based on payment. All businesses are displayed based on proximity to the route only.

### 2. **Accessibility-First**
Every route includes comprehensive accessibility information:
- Walking distances
- Stair counts
- Elevator availability
- Transfer requirements

### 3. **Cost Transparency**
Complete fare breakdowns showing:
- Base fares
- Transfer fees
- Zone charges
- Total cost per segment

### 4. **No Bias**
- Fixed listing fees for all businesses
- No sponsored results or advertisements
- Equal visual prominence for all listings

## 🚀 Getting Started

### Prerequisites

```bash
# Node.js 18+ and npm
node --version
npm --version
```

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/commutr.git
cd commutr

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env

# Start development server
npm run dev
```

### Configuration

Create a `.env` file with the following variables:

```env
# API Configuration
API_BASE_URL=http://localhost:3000
API_KEY=your_api_key_here

# Database
DATABASE_URL=your_database_url

# Transport Data Sources
TRANSPORT_API_KEY=your_transport_api_key
MAPS_API_KEY=your_maps_api_key

# Business Listings
LISTING_FEE_AMOUNT=50.00
PROXIMITY_THRESHOLD_METERS=500
```

## 📚 Documentation

Detailed documentation is available in the `.kiro/specs/commutr/` directory:

- **[Requirements Document](.kiro/specs/commutr/requirements.md)** - Complete user stories and acceptance criteria
- **[Design Document](.kiro/specs/commutr/design.md)** - Architecture, components, and correctness properties
- **[Process Flow Diagrams](.kiro/specs/commutr/)** - Visual representations of system workflows

## 🏗️ Project Structure

```
commutr/
├── .kiro/
│   └── specs/
│       └── commutr/
│           ├── requirements.md          # User stories & acceptance criteria
│           ├── design.md                # System design & architecture
│           ├── system-architecture.jpg  # Architecture diagram
│           ├── detailed-process-flow.jpg # Process flow diagram
│           └── *.dot                    # Graphviz source files
├── src/
│   ├── components/                      # React components
│   ├── services/                        # Business logic
│   │   ├── route-planner/
│   │   ├── fare-calculator/
│   │   ├── accessibility-analyzer/
│   │   ├── business-registry/
│   │   └── navigation-engine/
│   ├── models/                          # Data models
│   └── utils/                           # Utility functions
├── tests/                               # Unit and property-based tests
├── public/                              # Static assets
└── README.md
```

## 🧪 Testing

Commutr uses a dual testing approach:

### Unit Tests
```bash
npm test
```

### Property-Based Tests
```bash
npm run test:properties
```

We use [fast-check](https://github.com/dubzzz/fast-check) for property-based testing to verify correctness properties across all possible inputs.

## 🤝 Contributing

This repository is currently maintained by the project team.
Feedback and suggestions are welcome via issues.
This project is currently developed as part of the AWS AI for Bharat Hackathon.
Future development and open collaboration may be explored post-hackathon.




## 📋 Roadmap

- [ ] **Phase 1**: Core route planning and fare calculation
- [ ] **Phase 2**: Accessibility analysis engine
- [ ] **Phase 3**: Business registration and listing
- [ ] **Phase 4**: Navigation instructions (text & voice)
- [ ] **Phase 5**: Mobile app development
- [ ] **Phase 6**: Real-time updates and notifications
- [ ] **Phase 7**: Multi-language support

## 🐛 Known Issues

See the [Issues](https://github.com/YOUR_USERNAME/commutr/issues) page for a list of known issues and feature requests.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Anik Modak** - *Initial work* - [AnikModak](https://github.com/AnikModak)

## 🙏 Acknowledgments

- Public transport data providers
- Open-source community
- Contributors and testers

## 📞 Contact

- **Project Link**: [https://github.com/AnikModak/commutr](https://github.com/AnikModak/commutr)
- **Issues**: [https://github.com/AnikModak/commutr/issues](https://github.com/AnikModak/commutr/issues)

---

<p align="center">Made with ❤️ for commuters everywhere</p>
