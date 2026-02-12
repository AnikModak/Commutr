# Welcome to Commutr

Commutr is an open-source platform that helps commuters find optimal public transport routes based on cost and accessibility, while providing fair visibility to local businesses along the way.

## What Problem Does It Solve?

Public transport users face three main challenges:

1. **Cost Confusion**: Multiple route options with unclear pricing make it hard to find the cheapest way to travel
2. **Accessibility Barriers**: Limited information about stairs, walking distances, and transfers makes route planning difficult for people with mobility needs
3. **Business Discovery**: Local businesses struggle to reach commuters without expensive advertising

Commutr solves these by providing:
- Clear cost breakdowns for every route option
- Comprehensive accessibility information for all transport segments
- Neutral business listings based purely on proximity (no paid promotions)

## Who Is This For?

**Commuters**: Anyone using public transport who wants to save money and navigate accessible routes

**Business Owners**: Local shopkeepers seeking fair visibility along popular commuter routes

**Developers**: Contributors interested in public transport, accessibility, or ethical business models

## Key Features

- **Cost-Optimized Routing**: Automatically finds the cheapest combination of buses, trains, and transfers
- **Accessibility-First Design**: Shows stairs, elevators, walking distances, and transfer requirements for every route
- **Step-by-Step Navigation**: Text and voice instructions guide you through your journey
- **Neutral Business Listings**: Nearby businesses displayed by proximity only—no sponsored results
- **Transparent Pricing**: Complete fare breakdown including base fares, transfers, and zone charges

## High-Level Architecture

Commutr follows a modular architecture with five main layers:

```
User Interface (Web/Mobile)
         ↓
   API Gateway
         ↓
Core Services (Route Planning, Fare Calculation, Accessibility Analysis)
         ↓
  Data Layer (Transport Data, Business Listings)
         ↓
Cloud Infrastructure (AWS)
```

Each component has a single, well-defined responsibility and can be developed independently.

## Quick Links

- **[Project Vision & Goals](Project-Vision-&-Goals)** - Why we built this and where we're going
- **[Tech Stack & Tools](Tech-Stack-&-Tools)** - Technologies and why we chose them
- **[System Architecture](System-Architecture)** - Detailed component breakdown
- **[Setup & Installation](Setup-&-Installation)** - Get Commutr running locally
- **[Usage Guide](Usage-Guide)** - How to use the platform
- **[Contribution Guide](Contribution-Guide)** - How to contribute code
- **[Roadmap](Roadmap)** - Current status and future plans
- **[FAQ](FAQ)** - Common questions answered

## Getting Started

New to the project? Start here:

1. Read the [Project Vision & Goals](Project-Vision-&-Goals) to understand our philosophy
2. Check the [Tech Stack & Tools](Tech-Stack-&-Tools) to see what we're built with
3. Follow the [Setup & Installation](Setup-&-Installation) guide to run Commutr locally
4. Read the [Contribution Guide](Contribution-Guide) to start contributing

## Project Status

Commutr is currently in active development. Core route planning and fare calculation are functional. We're working on accessibility analysis and business registration features.

See the [Roadmap](Roadmap) for detailed progress and upcoming features.

## License

Commutr is released under the MIT License. See the LICENSE file in the repository for full details.

## Community

- **Issues**: Report bugs or request features on GitHub Issues
- **Discussions**: Join conversations about features and design decisions
- **Pull Requests**: Contribute code following our [Contribution Guide](Contribution-Guide)

---

*Last updated: 2026*
