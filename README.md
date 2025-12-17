# AWS Cost Calculator for Startups

> Cost estimation tool with physics-informed modeling, free tier analysis, and growth projections

##  Overview

A comprehensive AWS cost calculator specifically designed for startups. Unlike generic calculators, this tool provides:

- **Physics-informed modeling** - Uses computational models to account for scaling behavior and economies of scale
- **Startup-specific features** - Free tier tracking, AWS Activate credits, growth projections
- **Scenario comparison** - Compare On-Demand, Reserved, and Spot pricing
- **Smart workload profiles** - Pre-configured templates for common startup architectures
- **Export capabilities** - PDF reports and CSV breakdowns for team discussions

##  Features

### Core Calculator
- [x] 6 Workload profiles (Web App, Mobile Backend, SaaS, ML/AI, E-Commerce, Data Analytics)
- [x] Comprehensive service coverage (EC2, Lambda, Fargate, RDS, DynamoDB, S3, CloudFront, etc.)
- [x] Real-time cost calculation
- [x] Free Tier analysis (12-month benefit tracking)
- [x] AWS Activate credits integration
- [x] **Pricing Sources Tab** - Direct links to official AWS pricing pages for verification

### Advanced Features
- [x] **Scenario Comparison** - On-Demand vs Reserved (1yr/3yr) vs Spot instances
- [x] **Growth Projections** - 1, 6, and 12-month cost forecasts with user scaling
- [x] **Optimization Tips** - Context-aware recommendations based on configuration
- [x] **Export Options** - PDF reports and CSV data exports
- [x] **Shareable URLs** - URL parameter-based configuration sharing
- [x] **Live Pricing Verification** - Links to current AWS pricing (stays valid in 2027+)

### UI/UX
- [x] Dark terminal-inspired aesthetic
- [x] Smooth animations and transitions
- [x] Responsive design (mobile-friendly)
- [x] Tab-based navigation
- [x] Real-time updates

##  Quick Start

### Instant Deployment (No Build Required)

The calculator is a **single HTML file** - no dependencies, no build process, no backend.

#### Option 1: Open Locally
```bash
# Just open the file in any modern browser
open aws-cost-calculator.html
```

#### Option 2: Deploy to Vercel
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy (from the directory containing the HTML file)
vercel --prod
```

#### Option 3: Deploy to Netlify
```bash
# Via Netlify Drop
# Just drag and drop the HTML file to https://app.netlify.com/drop

# Or via CLI
npm i -g netlify-cli
netlify deploy --prod
```

#### Option 4: GitHub Pages
```bash
# Create a new repo, add the file, and enable GitHub Pages
git init
git add aws-cost-calculator.html
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/aws-cost-calculator.git
git push -u origin main

# Enable GitHub Pages in repo settings → Pages → Source: main branch
```

#### Option 5: AWS S3 Static Hosting
```bash
# Create S3 bucket
aws s3 mb s3://your-calculator-bucket

# Upload file
aws s3 cp aws-cost-calculator.html s3://your-calculator-bucket/index.html --acl public-read

# Enable static website hosting
aws s3 website s3://your-calculator-bucket --index-document index.html
```

##  Architecture

### Technical Stack
- **Frontend**: Pure React (via CDN) - No build process
- **Styling**: Custom CSS with CSS variables for theming
- **Charts**: Chart.js for visualizations (optional - loaded via CDN)
- **PDF Export**: jsPDF library (loaded via CDN)
- **State Management**: React Hooks (useState, useEffect)

### Design Philosophy

**1. Terminal-Inspired Aesthetics**
- Dark slate backgrounds (#0a0e1a)
- Electric cyan accents (#00e5ff)
- Monospace fonts (JetBrains Mono) for technical precision
- Animated grid background for depth

**2. Data-Driven UI**
- Cost values animate on change (scale + fade)
- Timeline visualization for growth
- Progress bars for visual cost comparison
- Color-coded badges (green=savings, amber=warning, red=danger)

**3. Zero-Configuration Deployment**
- No npm packages to install
- No build step required
- No backend or database needed
- Just open in browser or deploy to any static host

### File Structure
```
aws-cost-calculator.html      # Complete application (single file)
├── HTML structure
├── CSS styling
│   ├── Layout & components
│   ├── Animations
│   └── Responsive design
└── JavaScript (React)
    ├── Pricing data
    ├── Calculation engine
    ├── UI components
    └── Export functions
```

##  Pricing Model

### Hybrid Pricing Approach

This calculator uses a **hybrid model** to stay accurate over time:

1. **Baseline Pricing (Hardcoded)** - Fast calculations, works offline
   - Last verified: December 2025
   - Based on US East (N. Virginia) region
   - Allows instant estimates without API calls

2. **Verification Links (Dynamic)** - Always current
   - Direct links to official AWS pricing pages
   - Click "Pricing Sources" tab to verify current rates
   - Ensures calculator remains useful in 2027, 2028, and beyond

**Why This Works:**
- Calculator stays functional even if AWS APIs change
- Users can verify current prices anytime
- No backend required - pure static HTML
- Perfect balance of speed and accuracy

### Data Sources
All pricing is based on **US East (N. Virginia)** region:
- EC2 On-Demand pricing (t3 family)
- Lambda pricing (per request + compute)
- RDS pricing (db.t3 instances)
- DynamoDB on-demand pricing
- S3 Standard storage pricing
- CloudFront data transfer pricing

### Calculation Methodology

**1. Physics-Informed Scaling**
```javascript
// Growth projections use power law scaling
const multiplier = Math.pow(growthRate, month / 3);
const projectedCost = baseCost * multiplier * 0.85; // 15% efficiency gain
```

This accounts for:
- Economies of scale as infrastructure grows
- Improved resource utilization at higher loads
- Better caching effectiveness
- Connection pooling efficiency

**2. Free Tier Logic**
```javascript
// Example: EC2 free tier
if (showFreeTier && instanceSize === 't3_micro' && instances === 1) {
    savings += monthlyCost; // Full 750 hours covered
    actualCost = 0;
}
```

**3. Scenario Comparison**
- On-Demand: 100% base cost
- 1-Year Reserved: 70% of base (30% savings)
- 3-Year Reserved: 55% of base (45% savings)
- Spot Instances: 40% of base (60% savings, but interruptible)

##  Customization

### Branding

Update colors in the CSS `:root` variables:

```css
:root {
    --bg-primary: #0a0e1a;        /* Main background */
    --accent-cyan: #00e5ff;       /* Primary accent */
    --accent-blue: #2196f3;       /* Secondary accent */
    --accent-amber: #ffa726;      /* Warning color */
    --accent-emerald: #26a69a;    /* Success color */
}
```

### Adding Services

1. **Update Pricing Data**:
```javascript
const PRICING = {
    // ... existing services
    elasticbeanstalk: {
        environment_hour: 0.09,
    },
};
```

2. **Add to Calculation**:
```javascript
const calculateCosts = () => {
    // ... existing calculations
    if (config.elasticbeanstalk_enabled) {
        costs.other += PRICING.elasticbeanstalk.environment_hour * 730;
    }
};
```

3. **Add UI Control**:
```javascript
<div className="toggle-switch">
    <label className="switch">
        <input
            type="checkbox"
            checked={config.elasticbeanstalk_enabled}
            onChange={(e) => setConfig({
                ...config, 
                elasticbeanstalk_enabled: e.target.checked
            })}
        />
        <span className="slider"></span>
    </label>
    <label>Elastic Beanstalk</label>
</div>
```

### Adding Workload Profiles

```javascript
const WORKLOAD_PROFILES = {
    // ... existing profiles
    iot_platform: {
        name: 'IoT Platform',
        icon: '📡',
        desc: 'Connected devices',
        defaults: {
            compute_type: 'lambda',
            database_type: 'dynamodb',
            storage_gb: 200,
            traffic_gb: 500,
            lambda_requests: 10000000,
            iot_devices: 1000,
        }
    },
};
```

##  Export Features

### PDF Export
- Company branding support (update logo in code)
- Cost breakdown tables
- Configuration summary
- Recommendations section

### CSV Export
- Cost category breakdown
- Monthly and annual totals
- Importable into Excel/Google Sheets

### Shareable URLs
```javascript
// URL format
?workload=web_app&users=10000&compute=ec2&database=rds&storage=50&traffic=100&freeTier=true

// Generate share link
const shareUrl = `${window.location.origin}?${params}`;
```

##  Advanced Usage

### URL Parameters

Load pre-configured setups via URL:

```
https://yoursite.com/?workload=saas&users=50000&compute=fargate&database=rds&storage=500&traffic=2000&freeTier=false
```

Parameters:
- `workload`: web_app | mobile_backend | saas | ml_ai | ecommerce | data_analytics
- `users`: Monthly active users (number)
- `compute`: ec2 | lambda | fargate
- `database`: rds | dynamodb
- `storage`: Storage in GB (number)
- `traffic`: Monthly traffic in GB (number)
- `freeTier`: true | false

### Embedding

Embed the calculator in your website:

```html
<iframe 
    src="https://your-calculator-url.com" 
    width="100%" 
    height="1200px"
    frameborder="0"
    style="border-radius: 12px;">
</iframe>
```

##  Educational Use

### For Students
- Learn AWS service pricing structure
- Understand cloud cost optimization
- Explore different architecture patterns
- Practice cost-benefit analysis

### For Bootcamps
- Teaching cloud architecture fundamentals
- Demonstrating real-world cost considerations
- Comparing serverless vs traditional approaches
- Startup economics education

##  Roadmap

### Phase 1: Core Features 
- [x] Basic cost calculator
- [x] Workload profiles
- [x] Free tier calculation
- [x] Export to PDF/CSV

### Phase 2: Enhancements
- [ ] Real-time AWS Pricing API integration
- [ ] Multi-region pricing comparison
- [ ] Reserved Instance optimizer
- [ ] Savings Plans calculator
- [ ] Team collaboration features (requires backend)

### Phase 3: Advanced
- [ ] Historical cost tracking (requires database)
- [ ] Budget alerts and notifications
- [ ] Cost anomaly detection
- [ ] Architecture diagram generator
- [ ] Integration with AWS Cost Explorer

##  Contributing

This is designed as a portfolio/learning project, but contributions are welcome!

### Adding Features
1. Fork and create feature branch
2. Test thoroughly across browsers
3. Update README with new features
4. Submit PR with clear description

### Reporting Issues
- Browser compatibility issues
- Pricing inaccuracies
- UI/UX improvements
- Feature requests

##  License

MIT License - feel free to use, modify, and distribute.

##  FAQ

**Q: Why a single HTML file?**
A: Maximum accessibility. No build process, no dependencies, works anywhere. Perfect for quick deployments and demonstrations.

**Q: How accurate are the estimates?**
A: Pricing is based on current AWS rates for US East region. Real costs vary by region, usage patterns, and specific configurations. Always verify with AWS Pricing Calculator.

**Q: Can I use this for production planning?**
A: It's a good starting point, but for production, use AWS's official tools and consult with AWS Solutions Architects for complex deployments.

**Q: Does it work offline?**
A: Almost - the core calculator works, but PDF export and fonts require internet. You can download the external libraries for full offline functionality.

**Q: Can I customize the pricing data?**
A: Yes! The `PRICING` object at the top of the script is fully editable. Update it to match your negotiated rates or different regions.

**Q: Why React without JSX compilation?**
A: Using Babel Standalone allows React development without build tools. Great for learning and rapid prototyping.

##  Support

- Technical issues: Open a GitHub issue
- Feature requests: Start a discussion
- Questions: Check existing issues or ask in discussions

##  Use Cases

### For Founders
- Pitch deck cost slides
- Investor discussions
- Budget planning
- Architecture decisions

### For Consultants
- Client proposals
- Architecture reviews
- Cost optimization audits
- Migration planning

### For Developers
- Portfolio project
- Learning AWS pricing
- Architecture education
- Interview preparation

---

**Built with precision engineering principles** | **Physics-informed modeling** | **Startup-focused**

Created by [Elias Dan Phiri] - Cloud & AI Automation Consultant
