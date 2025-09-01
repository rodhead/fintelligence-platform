# Financial Intelligence Platform 🚀

## Overview

A cutting-edge financial management platform that helps users track spending, manage budgets, and achieve financial goals through AI-powered insights and automated financial planning.

### ✨ Key Features

- **🏦 Bank Integration**: Connect multiple bank accounts via Plaid API
- **📊 Smart Analytics**: AI-powered spending analysis and pattern detection
- **🎯 Goal Tracking**: Set and monitor financial goals with predictive completion dates
- **🤖 AI Financial Advisor**: Get personalized recommendations and insights
- **📈 Cashflow Forecasting**: ML-based predictions of future financial state
- **⚡ Real-time Alerts**: Instant notifications for unusual spending and goal milestones
- **👥 Peer Comparison**: Anonymous comparison with similar income brackets
- **🔒 Bank-grade Security**: End-to-end encryption and secure data handling

## 🏗 Architecture

### Technology Stack

#### Frontend
- **Angular 17+**: Modern web framework with TypeScript
- **NgRx**: State management
- **TailwindCSS**: Utility-first CSS framework
- **Chart.js**: Data visualization
- **PWA**: Progressive Web App capabilities

#### Backend Services
- **Java Spring Boot**: User Service, Banking Service, Notification Service
- **Python FastAPI**: Analytics Service, ML/AI Service
- **Node.js**: Real-time WebSocket connections

#### Databases
- **PostgreSQL**: Transactional data (users, accounts)
- **TimescaleDB**: Time-series data (transactions)
- **MongoDB**: Analytics and ML model storage
- **Redis**: Caching and session management

#### Infrastructure
- **Apache Kafka**: Event streaming and microservice communication
- **Docker & Kubernetes**: Containerization and orchestration
- **API Gateway**: Unified API entry point
- **Prometheus & Grafana**: Monitoring and metrics

### Microservices Architecture

```
┌─────────────────────────────────────────┐
│          Angular Frontend (PWA)          │
└─────────────────────┬───────────────────┘
                      │
              ┌───────▼────────┐
              │   API Gateway   │
              └───────┬────────┘
                      │
    ┌─────────────────┼─────────────────┐
    │                 │                 │
┌───▼────┐    ┌──────▼──────┐   ┌─────▼──────┐
│  User   │    │   Banking   │   │ Analytics  │
│ Service │    │   Service   │   │  Service   │
└─────────┘    └─────────────┘   └────────────┘
                      │
              ┌───────▼────────┐
              │  Apache Kafka   │
              └────────────────┘
```

## 🚀 Quick Start

### Prerequisites

- Docker & Docker Compose
- Node.js 18+ and npm
- Java 17+
- Python 3.11+
- Git

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/financial-intelligence-platform.git
cd financial-intelligence-platform
```

### 2. Environment Setup

```bash
# Copy environment template
cp .env.example .env

# Edit .env file with your credentials
nano .env
```

Required environment variables:
```env
# Database
DB_PASSWORD=your_secure_password
MONGO_PASSWORD=your_secure_password
REDIS_PASSWORD=your_secure_password

# Security
JWT_SECRET=your-256-bit-secret-key

# External APIs
PLAID_CLIENT_ID=your_plaid_client_id
PLAID_SECRET=your_plaid_secret
OPENAI_API_KEY=your_openai_api_key

# Email (Gmail)
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_app_password
```

### 3. Start with Docker Compose

```bash
# Build all services
docker-compose build

# Start all services
docker-compose up -d

# Check status
docker-compose ps

# View logs
docker-compose logs -f
```

### 4. Access the Application

- **Frontend**: http://localhost:4200
- **API Gateway**: http://localhost:8080
- **Kafka UI**: http://localhost:8090
- **Grafana**: http://localhost:3000 (admin/admin)
- **Kibana**: http://localhost:5601

## 📦 Development Setup

### Frontend Development

```bash
cd frontend
npm install
npm start
# Access at http://localhost:4200
```

### Backend Services

#### User Service (Java Spring Boot)
```bash
cd user-service
mvn clean install
mvn spring-boot:run
# Service runs on port 8081
```

#### Banking Service (Java Spring Boot)
```bash
cd banking-service
mvn clean install
mvn spring-boot:run
# Service runs on port 8082
```

#### Analytics Service (Python FastAPI)
```bash
cd analytics-service
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8083
```

### Database Migrations

```bash
# Run migrations
docker-compose exec postgres psql -U finplatform -d finplatform_db -f /migrations/up.sql

# Rollback migrations
docker-compose exec postgres psql -U finplatform -d finplatform_db -f /migrations/down.sql
```

## 🧪 Testing

### Run All Tests
```bash
# Unit tests
mvn test  # For Java services
pytest    # For Python services
npm test  # For Angular frontend

# Integration tests
./scripts/integration-tests.sh

# E2E tests
npm run e2e
```

### Test Coverage
```bash
# Generate coverage reports
mvn jacoco:report  # Java
pytest --cov=.     # Python
npm run test:coverage  # Angular
```

## 📊 API Documentation

### Authentication

All API endpoints require JWT authentication except `/api/auth/register` and `/api/auth/login`.

Include the token in the Authorization header:
```
Authorization: Bearer <your-jwt-token>
```

### Core Endpoints

#### User Management
```http
POST   /api/auth/register     # Register new user
POST   /api/auth/login        # Login
POST   /api/auth/refresh      # Refresh token
GET    /api/users/profile     # Get user profile
PUT    /api/users/profile     # Update profile
PUT    /api/users/preferences # Update preferences
```

#### Banking & Transactions
```http
POST   /api/banks/connect          # Connect bank account
GET    /api/banks/accounts         # List accounts
POST   /api/banks/sync-all         # Sync all accounts
GET    /api/transactions           # List transactions
POST   /api/transactions           # Create transaction
PUT    /api/transactions/{id}      # Update transaction
DELETE /api/transactions/{id}      # Delete transaction
POST   /api/transactions/import    # Import from file
POST   /api/transactions/categorize # Auto-categorize
```

#### Analytics & AI
```http
GET    /api/analytics/spending-patterns   # Spending analysis
GET    /api/analytics/cashflow-forecast   # Future predictions
GET    /api/analytics/goal-progress       # Goal tracking
POST   /api/analytics/stress-test         # Financial stress test
GET    /api/analytics/peer-comparison     # Peer benchmarking
POST   /api/ml/chat                       # AI advisor chat
GET    /api/ml/recommendations            # Get recommendations
POST   /api/ml/detect-anomalies          # Anomaly detection
```

#### Goals
```http
POST   /api/users/goals        # Create goal
GET    /api/users/goals        # List goals
PUT    /api/users/goals/{id}   # Update goal
DELETE /api/users/goals/{id}   # Delete goal
```

## 🚢 Production Deployment

### Kubernetes Deployment

```bash
# Create namespace
kubectl create namespace finplatform

# Apply configurations
kubectl apply -f k8s/

# Check deployment status
kubectl get pods -n finplatform

# Get service URLs
kubectl get services -n finplatform
```

### CI/CD Pipeline (GitHub Actions)

```yaml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Build and Push Docker Images
        run: |
          docker build -t finplatform/user-service:latest ./user-service
          docker push finplatform/user-service:latest
          
      - name: Deploy to Kubernetes
        run: |
          kubectl apply -f k8s/
          kubectl rollout status deployment/user-service -n finplatform
```

## 📈 Monitoring & Observability

### Metrics (Prometheus + Grafana)

1. Access Grafana: http://localhost:3000
2. Default credentials: admin/admin
3. Import dashboards from `monitoring/grafana/dashboards/`

### Logs (ELK Stack)

1. Access Kibana: http://localhost:5601
2. Create index pattern: `finplatform-*`
3. View logs in Discover tab

### Distributed Tracing (Jaeger)

1. Access Jaeger UI: http://localhost:16686
2. Select service to view traces
3. Analyze request flow across microservices

## 🔒 Security

### Security Features

- **JWT Token Authentication**: Secure API access
- **Password Hashing**: BCrypt with salt
- **Data Encryption**: AES-256 for sensitive data
- **HTTPS/TLS**: End-to-end encryption in transit
- **Rate Limiting**: API throttling to prevent abuse
- **Input Validation**: Comprehensive validation
- **SQL Injection Prevention**: Prepared statements
- **XSS Protection**: Content Security Policy

### Security Best Practices

1. **Regular Updates**: Keep dependencies updated
2. **Secret Management**: Use environment variables
3. **Audit Logging**: Track all sensitive operations
4. **Backup Strategy**: Regular automated backups
5. **Access Control**: Role-based permissions

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📝 License

This project is licensed under the MIT License - see [LICENSE.md](LICENSE.md) for details.

## 🆘 Troubleshooting

### Common Issues

#### Docker containers not starting
```bash
# Check logs
docker-compose logs [service-name]

# Restart services
docker-compose restart

# Clean rebuild
docker-compose down -v
docker-compose up --build
```

#### Database connection issues
```bash
# Check database is running
docker-compose ps postgres

# Test connection
docker-compose exec postgres psql -U finplatform -d finplatform_db
```

#### Kafka connection issues
```bash
# Check Kafka status
docker-compose exec kafka kafka-topics --bootstrap-server localhost:9092 --list

# Create topics manually if needed
docker-compose exec kafka kafka-topics --create --topic user-events --bootstrap-server localhost:9092
```

## 📞 Support

- **Documentation**: [docs.finplatform.com](https://docs.finplatform.com)
- **Issues**: [GitHub Issues](https://github.com/yourusername/financial-intelligence-platform/issues)
- **Email**: support@finplatform.com
- **Discord**: [Join our community](https://discord.gg/finplatform)

## 🙏 Acknowledgments

- Plaid for banking API integration
- OpenAI for AI capabilities
- The open-source community for amazing tools and libraries

---

**Built with ❤️ by the Financial Intelligence Platform Team**