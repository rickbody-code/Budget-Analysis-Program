# Developer Documentation - Budget Analysis Program

## Architecture Overview

The Budget Analysis Program is built as a client-side web application with AI integration for transaction categorization. The architecture prioritizes data privacy by processing all financial data locally in the browser.

## Project Structure

```
budget-analysis-program/
├── index.html              # Main application entry point
├── README.md              # Project documentation
├── developer.md           # This file
├── assets/
│   ├── css/
│   │   ├── main.css       # Core styles
│   │   ├── components.css # Component-specific styles
│   │   └── charts.css     # Visualization styles
│   ├── js/
│   │   ├── main.js        # Application entry point
│   │   ├── fileProcessor.js   # File upload and parsing
│   │   ├── dataProcessor.js   # Data cleaning and normalization
│   │   ├── aiIntegration.js   # AI API communication
│   │   ├── categorizer.js     # Transaction categorization logic
│   │   ├── chartGenerator.js  # Visualization generation
│   │   └── utils.js           # Utility functions
│   └── data/
│       ├── categories.json    # Default spending categories
│       └── merchantPatterns.json # Merchant name normalization patterns
├── components/
│   ├── upload.html        # File upload interface
│   ├── categories.html    # Category management
│   ├── review.html        # Transaction review interface
│   └── results.html       # Analysis results display
└── tests/
    ├── test-data/         # Sample CSV/Excel files for testing
    └── unit-tests/        # JavaScript unit tests
```

## Core Components

### 1. File Processor (`fileProcessor.js`)
**Purpose**: Handle file upload, validation, and parsing

**Key Functions**:
- `uploadFile(file)` - Process uploaded CSV/Excel files
- `validateFileFormat(file)` - Check file type and structure
- `parseCSV(data)` - Parse CSV using Papa Parse
- `parseExcel(file)` - Parse Excel using SheetJS
- `detectColumns(headers)` - Auto-detect date, amount, description columns

**Dependencies**:
- Papa Parse for CSV processing
- SheetJS for Excel processing

### 2. Data Processor (`dataProcessor.js`)
**Purpose**: Clean, filter, and normalize transaction data

**Key Functions**:
- `filterTransactions(transactions)` - Remove non-expenses (transfers, payments, etc.)
- `normalizeMerchantNames(transactions)` - Standardize merchant name variations
- `detectForeignTransactions(transactions)` - Identify overseas transactions
- `groupSimilarTransactions(transactions)` - Group by merchant and amount ranges
- `calculateAnnualProjection(transactions, monthsOfData)` - Scale to annual figures

**Filtering Rules**:
- Credit card payments (except interest)
- Inter-account transfers
- Bank fees
- Investment transfers
- Large ATM withdrawals (>$100, prompt user)

### 3. AI Integration (`aiIntegration.js`)
**Purpose**: Communicate with AI API for transaction categorization

**Key Functions**:
- `categorizeTransaction(transaction)` - Single transaction categorization
- `batchCategorize(transactions)` - Bulk transaction processing
- `generateConfidenceScore(transaction, category)` - Confidence scoring
- `improveWithFeedback(transaction, userCategory)` - Learn from user corrections

**API Structure**:
```javascript
{
  "transactions": [
    {
      "description": "WOOLWORTHS METRO",
      "amount": 47.32,
      "date": "2024-01-15"
    }
  ],
  "categories": ["Groceries", "Household", "Dining", "..."],
  "context": {
    "userPreferences": {},
    "previousCategorizations": {}
  }
}
```

### 4. Categorizer (`categorizer.js`)
**Purpose**: Manage category system and user interactions

**Key Functions**:
- `loadDefaultCategories()` - Load predefined categories
- `validateUserCategories(categories)` - Process user category selections
- `handleMultiVendorAllocation(vendor, transactions)` - Walmart-style percentage allocation
- `presentUncategorizedItems(transactions)` - Show items needing user input
- `applyUserFeedback(transaction, category)` - Process user categorizations

**Category Structure**:
```javascript
{
  "category": "Groceries",
  "subCategories": ["Supermarket", "Organic", "Convenience"],
  "keywords": ["woolworths", "coles", "iga"],
  "patterns": ["grocery", "supermarket"],
  "userDefined": false
}
```

### 5. Chart Generator (`chartGenerator.js`)
**Purpose**: Create visualizations and analysis reports

**Key Functions**:
- `generatePieChart(categoryData)` - Spending breakdown pie chart
- `generateBarChart(monthlyData)` - Monthly spending trends
- `generateCashflowChart(incomeExpenseData)` - Income vs expenses
- `createSummaryTable(categorizedData)` - Detailed spending table
- `generateInsights(data)` - AI-powered spending insights

## Data Flow

### 1. Upload Phase
```
File Upload → Validation → Parsing → Column Detection → Data Validation
```

### 2. Processing Phase
```
Raw Data → Filtering → Normalization → Foreign Detection → Grouping
```

### 3. Categorization Phase
```
Processed Data → AI Categorization → Confidence Scoring → User Review → Final Categories
```

### 4. Analysis Phase
```
Categorized Data → Aggregation → Annualization → Visualization → Insights
```

## Configuration

### AI API Configuration
```javascript
const AI_CONFIG = {
  apiUrl: 'https://api.example.com/categorize',
  apiKey: 'your-api-key',
  batchSize: 50,
  timeout: 30000,
  retryAttempts: 3
};
```

### Category Configuration
Located in `assets/data/categories.json`:
```json
{
  "expenses": [
    {
      "name": "Groceries",
      "keywords": ["woolworths", "coles", "supermarket"],
      "color": "#4CAF50"
    }
  ],
  "income": [
    {
      "name": "Salary",
      "keywords": ["payroll", "salary", "wages"],
      "color": "#2196F3"
    }
  ]
}
```

## Testing Strategy

### Unit Tests
- File parsing accuracy
- Data filtering correctness
- Merchant name normalization
- Category matching algorithms

### Integration Tests
- AI API communication
- End-to-end data flow
- Error handling scenarios

### Test Data
Sample files in `tests/test-data/`:
- `sample-bank-statement.csv`
- `sample-credit-card.xlsx`
- `complex-transactions.csv` (edge cases)

## Development Guidelines

### Code Style
- ES6+ features preferred
- Modular architecture
- Comprehensive error handling
- JSDoc documentation for all functions

### Security Considerations
- Client-side only processing
- No persistent data storage
- Secure API communication
- Input validation and sanitization

### Performance Optimization
- Lazy loading for large datasets
- Web Workers for heavy processing
- Efficient DOM manipulation
- Memory management for file processing

## API Integration

### Required Endpoints
1. **POST /categorize** - Transaction categorization
2. **POST /batch-categorize** - Bulk processing
3. **GET /categories** - Available categories
4. **POST /feedback** - User correction feedback

### Rate Limiting
- Implement client-side rate limiting
- Batch requests efficiently
- Handle API quotas gracefully

## Deployment

### Static Hosting
- GitHub Pages
- Netlify
- Vercel
- Any static file server

### Environment Variables
- `AI_API_KEY` - API key for AI service
- `AI_API_URL` - Base URL for AI service
- `ENVIRONMENT` - development/production

## Future Enhancements

### Short Term
- Mobile responsiveness
- Improved error messaging
- Export functionality (PDF, Excel)

### Long Term
- Multi-currency support
- Machine learning improvements
- User accounts and data persistence
- Advanced analytics and benchmarking
