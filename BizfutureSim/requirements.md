# BizFutureSim - Requirements Document

## 1. Functional Requirements

### 1.1 Core Features
- **Decision Input System**
  - Text input for business decision description
  - Dropdown selection for business type (paan shop, kirana store, mobile accessories, etc.)
  - Time horizon selection (3 months, 6 months, 1 year, 2 years)
  - Optional location input (city/area)
  - Optional investment range input

- **AI Simulation Engine**
  - Generate 3 scenarios: Best Case, Normal Case, Worst Case
  - Calculate probability percentages for each scenario
  - Assign risk levels (Low, Medium, High)
  - Provide clear explanations for each outcome

- **Results Display**
  - Visual representation of scenarios
  - Probability percentages with color coding
  - Risk assessment indicators
  - Detailed explanations for each scenario
  - Clear, non-technical language

### 1.2 User Interface Requirements
- Single-page web application
- Responsive design for desktop and mobile
- Clean, intuitive interface suitable for small business owners
- Form validation for required inputs
- Loading indicators during simulation processing

### 1.3 Business Logic Requirements
- Decision categorization (new business, expansion, inventory, services)
- Context-aware simulation based on business type and location
- Probabilistic modeling for scenario generation
- Risk assessment algorithms
- Explanation generation for each scenario

## 2. Technical Requirements

### 2.1 Frontend
- **Technologies**: HTML5, CSS3, JavaScript (ES6+)
- **Responsive Design**: Mobile-first approach
- **Browser Support**: Chrome, Firefox, Safari, Edge (latest versions)
- **Performance**: Page load time < 3 seconds

### 2.2 Backend
- **Framework**: Python Flask
- **API Design**: RESTful endpoints
- **Response Format**: JSON
- **Error Handling**: Proper HTTP status codes and error messages

### 2.3 AI/ML Components
- **Simulation Engine**: Rule-based probabilistic modeling
- **Decision Analysis**: Pattern matching and categorization
- **Scenario Generation**: Monte Carlo-style simulation
- **Explanation Engine**: Template-based reasoning output

## 3. API Specifications

### 3.1 Endpoints

#### POST /simulate
**Request Body:**
```json
{
  "decision": "Should I open a paan shop in my area?",
  "business_type": "paan_shop",
  "time_horizon": "6_months",
  "location": "Mumbai, Andheri",
  "investment_range": "50000-100000"
}
```

**Response:**
```json
{
  "scenarios": [
    {
      "type": "best_case",
      "probability": 25,
      "risk_level": "low",
      "outcome": "Monthly profit of ₹15,000-20,000",
      "explanation": "High foot traffic area with good demand for paan products"
    },
    {
      "type": "normal_case",
      "probability": 50,
      "risk_level": "medium",
      "outcome": "Monthly profit of ₹8,000-12,000",
      "explanation": "Average customer flow with seasonal variations"
    },
    {
      "type": "worst_case",
      "probability": 25,
      "risk_level": "high",
      "outcome": "Monthly loss of ₹2,000-5,000",
      "explanation": "Low demand or high competition in the area"
    }
  ],
  "overall_recommendation": "moderate_risk",
  "key_factors": ["location", "competition", "initial_investment"]
}
```

## 4. Data Requirements

### 4.1 Business Categories
- Paan Shop
- Kirana Store
- Mobile Accessories
- Tea Stall
- Fruit Vendor
- Stationery Shop
- Tailoring Services
- Beauty Parlor

### 4.2 Decision Types
- New Business Setup
- Business Expansion
- Inventory Increase
- Service Addition
- Location Change

### 4.3 Simulation Parameters
- Market demand factors
- Competition levels
- Seasonal variations
- Investment requirements
- Operating costs
- Revenue potential

## 5. Non-Functional Requirements

### 5.1 Performance
- API response time < 2 seconds
- Support for 100 concurrent users
- 99% uptime during demo periods

### 5.2 Security
- Input validation and sanitization
- No sensitive data storage
- HTTPS for production deployment

### 5.3 Usability
- Intuitive interface for non-technical users
- Clear error messages
- Accessible design (WCAG 2.1 AA compliance)

### 5.4 Scalability
- Modular architecture for easy feature additions
- Database-ready design for future data storage
- API versioning support

## 6. Constraints and Assumptions

### 6.1 Constraints
- MVP scope for hackathon timeline
- No real-time market data integration
- Static simulation models
- No user authentication required

### 6.2 Assumptions
- Users have basic understanding of their business domain
- Internet connectivity available
- Users can provide accurate input information
- English language interface sufficient for MVP

## 7. Success Criteria

### 7.1 MVP Success Metrics
- Functional demo with all core features
- Realistic scenario generation for 5+ business types
- User-friendly interface with form validation
- Working API with proper error handling
- Deployment-ready application

### 7.2 User Acceptance Criteria
- Users can input business decisions and receive scenarios
- Scenarios are realistic and well-explained
- Interface is intuitive for small business owners
- Results are displayed clearly with visual indicators
- System handles invalid inputs gracefully

## 8. Future Enhancements (Post-MVP)

### 8.1 Phase 2 Features
- User accounts and decision history
- Regional language support
- Mobile application
- Advanced AI models with machine learning

### 8.2 Phase 3 Features
- Real-time market data integration
- Voice input support
- Collaborative decision making
- Integration with business planning tools

## 9. Development Timeline (Hackathon)

### Day 1
- Project setup and basic frontend structure
- API endpoint design and Flask setup
- Core simulation logic implementation

### Day 2
- Frontend-backend integration
- Scenario generation algorithms
- UI/UX refinement and testing

### Day 3
- Final testing and bug fixes
- Demo preparation and deployment
- Documentation and presentation materials