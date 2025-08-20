# Budget Analysis Program

An AI-powered budget analysis tool that automatically categorizes 6-12 months of financial data to provide comprehensive spending insights and cashflow analysis.

## Features

- **Automated Transaction Categorization**: AI-powered categorization with confidence scoring
- **Smart Data Processing**: Filters out transfers, normalizes merchant names
- **User-Friendly Category Management**: Custom categories with sample transaction previews
- **Multi-Vendor Intelligence**: Handles stores like Walmart with percentage-based allocation
- **Foreign Transaction Handling**: Groups overseas spending by date ranges
- **Comprehensive Analysis**: Spending breakdowns, trends, and benchmark comparisons
- **Cashflow Insights**: Income vs expense analysis with projections

## How It Works

1. **Upload Data**: Import 6-12 months of credit card and banking files (CSV/Excel)
2. **Validate Categories**: Review and customize spending categories
3. **AI Processing**: Automatic transaction categorization with smart grouping
4. **User Assistance**: Help categorize unclear transactions (>5% threshold)
5. **Analysis & Visualization**: Generate charts, tables, and spending insights

## Technical Stack

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **File Processing**: Papa Parse (CSV), SheetJS (Excel)
- **AI Integration**: External API for transaction categorization
- **Visualization**: Chart.js or similar charting library
- **Data Handling**: Client-side processing (no server required)

## Getting Started

### Prerequisites
- Modern web browser with JavaScript enabled
- AI API key for transaction categorization

### Installation
1. Clone the repository
```bash
git clone https://github.com/yourusername/budget-analysis-program.git
cd budget-analysis-program
```

2. Open `index.html` in your browser
3. Configure your AI API key in the settings

### Usage
1. **Upload Files**: Select your bank/credit card CSV or Excel files
2. **Review Categories**: Customize spending categories to match your needs
3. **Process Data**: Let AI categorize your transactions
4. **Review Results**: Examine spending breakdown and insights
5. **Export**: Save your analysis for future reference

## Supported File Formats

- **CSV Files**: Bank statements, credit card exports
- **Excel Files**: .xlsx, .xls formats
- **Currency**: AUD accounts (Australian Dollar)

## Data Privacy

- **Client-Side Processing**: All data processing happens in your browser
- **No Data Storage**: Files are not uploaded to servers
- **API Usage**: Only transaction descriptions sent to AI API for categorization

## Development Roadmap

### Phase 1: Core Engine ✅
- [x] File upload and parsing
- [x] Data cleaning and merchant normalization
- [x] Basic AI categorization
- [x] User category validation

### Phase 2: Advanced Features 🚧
- [ ] Multi-vendor percentage allocation
- [ ] Foreign transaction handling
- [ ] Recurring payment detection
- [ ] Confidence scoring system

### Phase 3: Analysis & Insights 📋
- [ ] Advanced visualizations
- [ ] Benchmark comparisons
- [ ] Trend analysis
- [ ] Cashflow projections

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For questions, issues, or feature requests, please open an issue on GitHub.

---

**Note**: This application handles sensitive financial data. Always ensure you're using the latest version and follow security best practices.
