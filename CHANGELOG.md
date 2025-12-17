# AWS Cost Calculator - Changelog

## Version 1.2 - December 2025

### Major Update: Future-Proof Pricing

**Problem Solved:** Hardcoded pricing becomes outdated. Someone viewing this calculator in 2027 would get inaccurate estimates.

**Solution:** Added comprehensive pricing verification system.

### Added
- **Pricing Sources Tab** - New dedicated tab with direct links to all official AWS pricing pages
  - EC2, Lambda, RDS, DynamoDB, S3, CloudFront, ElastiCache, SES pricing
  - Links to AWS Pricing Calculator
  - Links to AWS Free Tier details
- **Pricing Freshness Warning** - Prominent notice showing when pricing was last verified
- **Verification Guide** - Step-by-step instructions on how to check current AWS pricing
- **Pricing Change Frequency Info** - Educational content about how often AWS updates prices

### Enhanced
- **Header Notice** - Now links to Pricing Sources tab instead of external calculator
- **Navigation** - Added 5th tab for "Pricing Sources"
- **Footer Timestamp** - Updated to December 2025
- **Documentation** - README now explains hybrid pricing approach

### Benefits
- Calculator remains useful in 2027+ with verification links
- Users can instantly check if prices have changed
- No backend required - maintains pure static architecture
- Educational - teaches users about AWS pricing structure

---

## Version 1.1 - December 2024

### Added
- **Pricing Data Timestamp** - Header now displays "Pricing Data Last Updated: January 2025"
- **Regional Indicator** - Clear indication that pricing is for US East (N. Virginia)
- **Accuracy Notice** - Prominent note about ±10-15% estimate accuracy
- **Comprehensive Footer** - Detailed breakdown of what's included/excluded in estimates

### Enhanced
- **Header Pricing Info** - Added inline notice with link to AWS Pricing Calculator
- **Footer Information** - Expanded footer with:
  - What's included in estimates (✓)
  - Estimate accuracy range (⚡)
  - What's not included (✗)
  - Regional variance information
  - Production planning disclaimer

### Improved Transparency
- Users now immediately see when pricing data was last updated
- Clear expectations about estimate accuracy
- Links to official AWS Pricing Calculator for verification
- Explicit list of costs not included (Multi-AZ, NAT Gateway, etc.)

---

## Version 1.0 - December 2024

### Initial Release
- 6 workload profiles (Web App, Mobile Backend, SaaS, ML/AI, E-Commerce, Data Analytics)
- Comprehensive AWS service coverage (EC2, Lambda, Fargate, RDS, DynamoDB, S3, CloudFront)
- Free Tier tracking and calculations
- AWS Activate credits integration ($1K-$100K)
- Growth projections (1, 6, 12 months)
- Scenario comparison (On-Demand, Reserved 1yr/3yr, Spot)
- Context-aware optimization tips
- PDF export functionality
- CSV export functionality
- Shareable URLs via query parameters
- Responsive mobile design
- Dark terminal-inspired theme
- Physics-informed cost scaling model

---

## Pricing Data Sources

All pricing based on publicly available AWS pricing pages as of January 2025:
- EC2 On-Demand Pricing: https://aws.amazon.com/ec2/pricing/on-demand/
- Lambda Pricing: https://aws.amazon.com/lambda/pricing/
- RDS Pricing: https://aws.amazon.com/rds/pricing/
- S3 Pricing: https://aws.amazon.com/s3/pricing/
- DynamoDB Pricing: https://aws.amazon.com/dynamodb/pricing/
- CloudFront Pricing: https://aws.amazon.com/cloudfront/pricing/

**Region:** US East (N. Virginia) - us-east-1

---

## Known Limitations

1. **Regional Pricing** - Only US East (N. Virginia) pricing included
2. **Multi-AZ Not Included** - RDS Multi-AZ deployments cost ~2x (not calculated)
3. **Data Transfer Simplified** - Tiered pricing not fully modeled
4. **Storage Costs** - EBS volumes for EC2 not separately itemized
5. **Network Costs** - NAT Gateway, VPC, Transit Gateway not included
6. **Support Plans** - Developer, Business, Enterprise support not included
7. **Reserved Instance Savings** - Estimates based on typical savings percentages

---

## Future Enhancements

### Planned for v1.2
- [ ] Region selector with pricing multipliers
- [ ] Multi-AZ toggle for RDS
- [ ] Storage cost breakdown (separate EBS/RDS storage)
- [ ] Data transfer tier calculator
- [ ] Support plan cost estimator

### Planned for v2.0
- [ ] Real-time AWS Pricing API integration
- [ ] Historical pricing trends
- [ ] Team collaboration features (requires backend)
- [ ] Saved configurations (requires backend)
- [ ] Cost alerts and budgets
- [ ] Architecture diagram generator

### Under Consideration
- [ ] Azure/GCP comparison mode
- [ ] FinOps best practices guide
- [ ] Integration with AWS Cost Explorer
- [ ] Terraform cost estimation from IaC files
- [ ] Well-Architected Framework cost checks

---

## Maintenance Schedule

- **Quarterly**: Review and update AWS pricing data
- **Monthly**: Monitor AWS pricing changes and announcements
- **As Needed**: Update when AWS introduces new instance types or services

---

## Contributing

Found outdated pricing? Want to add a feature? 

1. Check the pricing sources above for current AWS rates
2. Update the `PRICING` object in the JavaScript
3. Update the "Last Updated" date in header and footer
4. Test calculations with known scenarios
5. Submit PR with detailed changes

---

## Version History

| Version | Date | Key Changes |
|---------|------|-------------|
| 1.1 | Dec 2025 | Added pricing transparency features |
| 1.0 | Dec 2025 | Initial public release |

---

## Support

Questions about pricing accuracy?
- Verify with [AWS Pricing Calculator](https://calculator.aws/)
- Check [AWS Pricing Documentation](https://aws.amazon.com/pricing/)
- Contact AWS Solutions Architects for production planning

---

**Disclaimer:** This calculator is provided as-is for informational purposes. Pricing data is subject to change without notice. Always verify costs with official AWS sources before making purchasing decisions.
