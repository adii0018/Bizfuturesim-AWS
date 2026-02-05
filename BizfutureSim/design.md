# BizFutureSim - Design Document

## 1. System Architecture

### 1.1 High-Level Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend      │    │  AI Simulation  │
│   (HTML/CSS/JS) │◄──►│   (Flask API)   │◄──►│     Engine      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### 1.2 Component Architecture
```
Frontend Layer:
├── Input Form Component
├── Results Display Component
├── Loading/Error Components
└── Responsive Layout

Backend Layer:
├── Flask Application
├── API Routes
├── Input Validation
└── Response Formatting

AI Engine:
├── Decision Analyzer
├── Scenario Generator
├── Probability Calculator
└── Explanation Engine
```

## 2. Database Design (Future Enhancement)

### 2.1 Entity Relationship
```
Business_Types          Decisions               Scenarios
├── id                 ├── id                  ├── id
├── name               ├── decision_text       ├── decision_id
├── category           ├── business_type_id    ├── scenario_type
├── risk_factors       ├── time_horizon        ├── probability
└── market_data        ├── location            ├── risk_level
                       ├── investment_range    ├── outcome
                       └── created_at          └── explanation
```

### 2.2 Sample Data Structure
```json
{
  "business_types": {
    "paan_shop": {
      "category": "retail",
      "avg_investment": "30000-80000",
      "success_rate": 0.65,
      "risk_factors": ["location", "competition", "regulations"],
      "seasonal_impact": "medium"
    }
  }
}
```

## 3. User Interface Design

### 3.1 Page Layout
```
┌─────────────────────────────────────────────────────────┐
│                    Header                               │
│              BizFutureSim Logo                          │
│           "See the future before you invest"           │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌─────────────────┐  ┌─────────────────────────────┐   │
│  │   Input Form    │  │     Results Panel           │   │
│  │                 │  │                             │   │
│  │ • Decision Text │  │  ┌─────────────────────┐    │   │
│  │ • Business Type │  │  │   Best Case         │    │   │
│  │ • Time Horizon  │  │  │   25% Probability   │    │   │
│  │ • Location      │  │  └─────────────────────┘    │   │
│  │ • Investment    │  │                             │   │
│  │                 │  │  ┌─────────────────────┐    │   │
│  │ [Simulate]      │  │  │   Normal Case       │    │   │
│  └─────────────────┘  │  │   50% Probability   │    │   │
│                       │  └─────────────────────┘    │   │
│                       │                             │   │
│                       │  ┌─────────────────────┐    │   │
│                       │  │   Worst Case        │    │   │
│                       │  │   25% Probability   │    │   │
│                       │  └─────────────────────┘    │   │
│                       └─────────────────────────────┘   │
├─────────────────────────────────────────────────────────┤
│                    Footer                               │
└─────────────────────────────────────────────────────────┘
```

### 3.2 Color Scheme
```css
:root {
  --primary-color: #2563eb;      /* Blue */
  --success-color: #16a34a;      /* Green */
  --warning-color: #d97706;      /* Orange */
  --danger-color: #dc2626;       /* Red */
  --neutral-color: #6b7280;      /* Gray */
  --background: #f8fafc;         /* Light Gray */
  --text-primary: #1f2937;       /* Dark Gray */
  --text-secondary: #6b7280;     /* Medium Gray */
}
```

### 3.3 Typography
```css
/* Primary Font: Inter (Clean, Professional) */
font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;

/* Headings */
h1: 2.5rem, font-weight: 700
h2: 2rem, font-weight: 600
h3: 1.5rem, font-weight: 600

/* Body Text */
body: 1rem, font-weight: 400
small: 0.875rem, font-weight: 400
```

## 4. Component Design Specifications

### 4.1 Input Form Component
```html
<div class="input-form">
  <div class="form-group">
    <label>Business Decision</label>
    <textarea placeholder="e.g., Should I open a paan shop in my area?"></textarea>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label>Business Type</label>
      <select>
        <option>Paan Shop</option>
        <option>Kirana Store</option>
        <!-- ... -->
      </select>
    </div>
    
    <div class="form-group">
      <label>Time Horizon</label>
      <select>
        <option>3 Months</option>
        <option>6 Months</option>
        <!-- ... -->
      </select>
    </div>
  </div>
  
  <button class="simulate-btn">Simulate Future</button>
</div>
```

### 4.2 Scenario Card Component
```html
<div class="scenario-card best-case">
  <div class="scenario-header">
    <h3>Best Case Scenario</h3>
    <div class="probability-badge">25%</div>
  </div>
  
  <div class="risk-indicator low-risk">
    <span class="risk-dot"></span>
    Low Risk
  </div>
  
  <div class="outcome">
    <h4>Expected Outcome</h4>
    <p>Monthly profit of ₹15,000-20,000</p>
  </div>
  
  <div class="explanation">
    <h4>Why This Could Happen</h4>
    <p>High foot traffic area with good demand for paan products...</p>
  </div>
</div>
```

### 4.3 Loading States
```html
<!-- Loading Animation -->
<div class="loading-container">
  <div class="spinner"></div>
  <p>Analyzing your decision...</p>
  <p class="loading-step">Generating scenarios...</p>
</div>

<!-- Progress Indicator -->
<div class="progress-bar">
  <div class="progress-fill" style="width: 60%"></div>
</div>
```

## 5. API Design

### 5.1 Request/Response Flow
```
User Input → Validation → Decision Analysis → Scenario Generation → Response
```

### 5.2 Error Handling
```json
{
  "error": true,
  "message": "Invalid business type selected",
  "code": "INVALID_BUSINESS_TYPE",
  "details": {
    "field": "business_type",
    "allowed_values": ["paan_shop", "kirana_store", "mobile_accessories"]
  }
}
```

### 5.3 API Endpoints Structure
```
POST /api/simulate
├── Input Validation
├── Decision Categorization
├── Context Analysis
├── Scenario Generation
└── Response Formatting

GET /api/business-types
└── Returns available business categories

GET /api/health
└── System health check
```

## 6. AI Simulation Engine Design

### 6.1 Decision Analysis Pipeline
```
Input Decision Text
    ↓
Keyword Extraction
    ↓
Business Category Detection
    ↓
Risk Factor Identification
    ↓
Context Parameter Mapping
    ↓
Scenario Generation
```

### 6.2 Probability Calculation Logic
```python
def calculate_probabilities(business_type, location, investment, time_horizon):
    base_success_rate = BUSINESS_DATA[business_type]['success_rate']
    
    # Location factor
    location_multiplier = get_location_factor(location)
    
    # Investment factor
    investment_factor = calculate_investment_impact(investment, business_type)
    
    # Time horizon factor
    time_factor = get_time_horizon_impact(time_horizon)
    
    # Calculate scenario probabilities
    normal_case = base_success_rate * location_multiplier * investment_factor
    best_case = normal_case * 0.4  # 40% of normal case probability
    worst_case = 1 - normal_case - best_case
    
    return normalize_probabilities(best_case, normal_case, worst_case)
```

### 6.3 Scenario Templates
```json
{
  "paan_shop": {
    "best_case": {
      "outcome_template": "Monthly profit of ₹{min_profit}-{max_profit}",
      "explanation_template": "High foot traffic area with good demand for paan products. Strategic location near offices/colleges ensures steady customer flow."
    },
    "normal_case": {
      "outcome_template": "Monthly profit of ₹{min_profit}-{max_profit}",
      "explanation_template": "Average customer flow with seasonal variations. Moderate competition but stable local demand."
    },
    "worst_case": {
      "outcome_template": "Monthly loss of ₹{min_loss}-{max_loss}",
      "explanation_template": "Low demand or high competition in the area. Regulatory issues or changing customer preferences may impact business."
    }
  }
}
```

## 7. Responsive Design Specifications

### 7.1 Breakpoints
```css
/* Mobile First Approach */
.container {
  /* Mobile: 320px - 768px */
  padding: 1rem;
  
  /* Tablet: 768px - 1024px */
  @media (min-width: 768px) {
    padding: 2rem;
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 2rem;
  }
  
  /* Desktop: 1024px+ */
  @media (min-width: 1024px) {
    max-width: 1200px;
    margin: 0 auto;
  }
}
```

### 7.2 Mobile Optimizations
- Touch-friendly button sizes (minimum 44px)
- Simplified navigation
- Stacked layout for form and results
- Swipeable scenario cards
- Optimized font sizes for readability

## 8. Performance Considerations

### 8.1 Frontend Optimizations
- Minified CSS/JS files
- Image optimization and lazy loading
- Efficient DOM manipulation
- Debounced input validation
- Local caching of business type data

### 8.2 Backend Optimizations
- Response compression (gzip)
- Efficient JSON serialization
- Input validation caching
- Optimized simulation algorithms
- Connection pooling for future database integration

## 9. Security Design

### 9.1 Input Validation
```python
def validate_input(data):
    # Sanitize text inputs
    decision_text = sanitize_text(data.get('decision', ''))
    
    # Validate business type
    if data.get('business_type') not in ALLOWED_BUSINESS_TYPES:
        raise ValidationError("Invalid business type")
    
    # Validate investment range
    investment = validate_investment_range(data.get('investment_range'))
    
    return validated_data
```

### 9.2 Security Headers
```python
@app.after_request
def after_request(response):
    response.headers['X-Content-Type-Options'] = 'nosniff'
    response.headers['X-Frame-Options'] = 'DENY'
    response.headers['X-XSS-Protection'] = '1; mode=block'
    return response
```

## 10. Testing Strategy

### 10.1 Frontend Testing
- Unit tests for utility functions
- Component testing for form validation
- Integration tests for API calls
- Cross-browser compatibility testing
- Mobile responsiveness testing

### 10.2 Backend Testing
- API endpoint testing
- Input validation testing
- Simulation logic testing
- Error handling testing
- Performance testing

## 11. Deployment Architecture

### 11.1 Development Environment
```
Local Development:
├── Frontend: Live Server (VS Code)
├── Backend: Flask Development Server
└── Testing: Manual testing + Postman
```

### 11.2 Production Deployment
```
Production Stack:
├── Frontend: Static hosting (Netlify/Vercel)
├── Backend: Cloud hosting (Heroku/Railway)
├── Domain: Custom domain with HTTPS
└── Monitoring: Basic error logging
```

## 12. Future Enhancements Design

### 12.1 Advanced AI Features
- Machine learning model integration
- Real-time market data analysis
- Personalized recommendations
- Historical decision tracking

### 12.2 User Experience Improvements
- Interactive scenario visualization
- Comparison tools for multiple decisions
- Export functionality for reports
- Collaborative decision making features