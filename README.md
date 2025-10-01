# AWS Auto Scaling Workshop

A comprehensive hands-on workshop for deploying scalable applications using Amazon EC2 Auto Scaling and Elastic Load Balancing.

## 🎯 Overview

This workshop demonstrates how to deploy the FCJ Management application with Amazon EC2 Auto Scaling to ensure dynamic scalability based on fluctuating workloads. You'll implement Elastic Load Balancing to distribute traffic and efficiently manage user requests to your application tier.

## 🏗️ Architecture

The workshop implements a multi-tier architecture following AWS Well-Architected Framework principles:

- **Web Tier**: Auto Scaling Group with EC2 instances behind an Application Load Balancer
- **Database Tier**: Amazon RDS for persistent data storage
- **Network**: VPC with public/private subnets across multiple Availability Zones

## 📚 Workshop Modules

1. **[Introduction](content/1-introduction/)** - Auto Scaling concepts and scaling strategies
2. **[Preparation](content/2-preparation/)** - Infrastructure setup and prerequisites
3. **[Create Launch Template](content/3-create-launch-template/)** - EC2 instance configuration template
4. **[Setup Load Balancer](content/4-setup-load-balancer/)** - Application Load Balancer and Target Groups
5. **[Test](content/5-test/)** - Initial testing and validation
6. **[Create Auto Scaling Group](content/6-create-auto-scaling-group/)** - Auto Scaling Group configuration
7. **[Test Solutions](content/7-test-solutions/)** - Testing different scaling strategies
8. **[Cleanup](content/8-Cleanup/)** - Resource cleanup and cost optimization

## 🚀 Quick Start

### Prerequisites

- AWS Account with appropriate permissions
- Hugo static site generator (for local development)
- Basic understanding of AWS services (EC2, VPC, RDS, ELB)

### Local Development

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd 000006-AutoScaling
   ```

2. **Install Hugo** (if not already installed)
   ```bash
   # macOS
   brew install hugo
   
   # Ubuntu/Debian
   sudo apt-get install hugo
   
   # Windows
   choco install hugo
   ```

3. **Start the development server**
   ```bash
   hugo server -D
   ```

4. **Access the workshop**
   Open your browser to `http://localhost:1313`

### Build for Production

```bash
hugo --minify
```

The generated site will be in the `public/` directory.

## 🔧 Scaling Strategies Covered

### 1. Manual Scaling
- Manually adjust instance count based on anticipated demand
- Requires human intervention
- Best for predictable, scheduled events

### 2. Dynamic Scaling
- **Target Tracking**: Maintain specific metric values (e.g., 50% CPU)
- **Step Scaling**: Proportional adjustments based on metric thresholds
- **Simple Scaling**: Single metric threshold-based scaling

### 3. Scheduled Scaling
- Time-based scaling for predictable patterns
- Business hours vs. off-hours capacity adjustment
- Cost optimization through proactive scaling

### 4. Predictive Scaling
- Machine learning-based capacity forecasting
- Proactive scaling based on historical patterns
- Optimal performance during anticipated traffic spikes

## 📁 Project Structure

```
000006-AutoScaling/
├── content/                    # Workshop content (Markdown)
│   ├── 1-introduction/        # Auto Scaling concepts
│   ├── 2-preparation/         # Infrastructure setup
│   ├── 3-create-launch-template/
│   ├── 4-setup-load-balancer/
│   ├── 5-test/
│   ├── 6-create-auto-scaling-group/
│   ├── 7-test-solutions/      # Scaling strategy tests
│   └── 8-Cleanup/            # Resource cleanup
├── static/                    # Static assets (images, CSS)
├── themes/                    # Hugo theme
├── layouts/                   # Custom layout overrides
├── config.toml               # Hugo configuration
└── README.md                 # This file
```

## 🌐 Multi-language Support

The workshop supports both English and Vietnamese:

- **English**: Default language
- **Vietnamese**: Available through language switcher

## 🔒 Security Best Practices

The workshop implements:

- Network segmentation with VPC and subnets
- Security groups with least privilege access
- SSL/TLS termination at the load balancer
- Encrypted data transmission
- IAM roles and policies following principle of least privilege

## 💰 Cost Optimization

- Auto Scaling reduces costs during low-demand periods
- Scheduled scaling for predictable patterns
- Proper resource cleanup procedures included
- Monitoring and alerting for cost management

## 🛠️ Customization

### Theme Customization

The workshop uses the `hugo-theme-learn` theme with custom styling:

- **Theme variant**: `workshop` (defined in `config.toml`)
- **Custom CSS**: Located in `static/css/`
- **Custom layouts**: Override in `layouts/` directory

### Content Modification

1. Edit Markdown files in the `content/` directory
2. Add images to `static/images/`
3. Update navigation in `config.toml`

## 📊 Monitoring and Metrics

The workshop covers:

- CloudWatch metrics for Auto Scaling decisions
- Custom metrics for application-specific scaling
- Alarms and notifications
- Performance monitoring best practices

## 🔄 CI/CD Integration

The project includes:

- `.gitignore` for Hugo-specific files
- Git submodules for theme management
- Build artifacts exclusion

## 🆘 Troubleshooting

### Common Issues

1. **Hugo build fails**
   - Check Hugo version compatibility
   - Verify theme submodule initialization

2. **Images not displaying**
   - Ensure images are in `static/images/`
   - Check image paths in Markdown files

3. **Theme not loading**
   - Initialize git submodules: `git submodule update --init --recursive`

## 📖 Additional Resources

- [AWS Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/)
- [Elastic Load Balancing Guide](https://docs.aws.amazon.com/elasticloadbalancing/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Hugo Documentation](https://gohugo.io/documentation/)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test locally with `hugo server`
5. Submit a pull request

## 📄 License

This project is licensed under the MIT-0 License - see the [LICENSE](LICENSE) file for details.

## 🏷️ Tags

`aws` `auto-scaling` `elastic-load-balancing` `ec2` `workshop` `hugo` `cloud-computing` `infrastructure` `scalability` `high-availability`

---

**Part of the AWS First Cloud Journey series** - [Visit the main site](https://cloudjourney.awsstudygroup.com)
