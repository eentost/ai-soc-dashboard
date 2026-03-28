# AI-SOC Dashboard

**AI-powered Security Operations Center (SOC) Dashboard** with real-time threat detection, anomaly detection using machine learning, and Docker Compose infrastructure.

## 🎯 Features

- **Real-time Threat Detection**: AI-powered anomaly detection using Isolation Forest and other ML models
- **Multi-source Log Ingestion**: Integration with Elasticsearch and ClickHouse for centralized log storage
- **Interactive Dashboard**: React-based UI on port **5178** for visualization and analysis
- **Go Backend API**: High-performance REST API on port 20006
- **Docker Compose Setup**: One-command deployment of entire stack
- **ML-based Threat Detection**: Python-based threat detection service
- **ELK Stack**: Elasticsearch for indexing, Kibana for exploration
- **ClickHouse**: OLAP database for large-scale analytics (port 20001)

## 📋 Architecture

```
┌─────────────────────────────────────────────────┐
│         AI-SOC Dashboard Frontend (5178)        │
│                  React + Nginx                   │
└────────────────┬────────────────────────────────┘
                 │
                 ↓
┌─────────────────────────────────────────────────┐
│         Go Backend API (20006)                  │
│        REST API + Business Logic                │
└─┬──────────────┬─────────────┬──────────────┬──┘
  │              │             │              │
  ↓              ↓             ↓              ↓
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│Elastic   │ │ClickHouse│ │  Redis   │ │  Python  │
│search    │ │(20001-2) │ │ (20005)  │ │  ML Svc  │
│(20003-4) │ │          │ │  Cache   │ │ (Threat  │
│          │ │ OLAP DB  │ │          │ │ Detection│
└──────────┘ └──────────┘ └──────────┘ └──────────┘
```

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Git

### Installation & Deployment

```bash
# Clone the repository
git clone https://github.com/eentost/ai-soc-dashboard.git
cd ai-soc-dashboard

# Start all services
docker-compose up -d

# Monitor logs
docker-compose logs -f
```

## 🔌 Service Ports & URLs

| Service | Port | URL | Purpose |
|---------|------|-----|----------|
| React Dashboard | 5178 | http://localhost:5178 | Main UI |
| Go Backend API | 20006 | http://localhost:20006 | REST API |
| Elasticsearch | 20003 | http://localhost:20003 | Log storage |
| ClickHouse HTTP | 20001 | http://localhost:20001 | OLAP queries |
| ClickHouse Native | 20002 | localhost:20002 | Native protocol |
| Redis | 20005 | localhost:20005 | Cache layer |
| Kibana | 20007 | http://localhost:20007 | ES visualization |

## 📁 Project Structure

```
ai-soc-dashboard/
├── docker-compose.yml       # Service orchestration
├── backend/                 # Go backend service
│   ├── Dockerfile
│   ├── go.mod
│   └── go.sum
├── frontend/                # React dashboard
│   ├── Dockerfile
│   └── package.json
├── ml_service/              # Python ML service
│   ├── Dockerfile
│   └── requirements.txt
└── README.md
```

## 🛠️ Tech Stack

- **Frontend**: React, Nginx
- **Backend**: Go (Chi router, Elasticsearch client, ClickHouse driver)
- **Database**: Elasticsearch (search), ClickHouse (analytics)
- **Cache**: Redis
- **ML**: Python (scikit-learn, XGBoost)
- **Containerization**: Docker & Docker Compose

## 📊 Data Flow

1. **Log Ingestion**: Raw security logs ingested into Elasticsearch
2. **Analysis**: ClickHouse performs OLAP analytics
3. **Threat Detection**: ML service identifies anomalies in real-time
4. **Visualization**: React dashboard displays threats and metrics
5. **Caching**: Redis caches frequent queries for performance

## 🤖 ML Models

- **Isolation Forest**: Anomaly detection for network traffic
- **Autoencoder**: Pattern recognition in behavioral data
- **Time Series Analysis**: Detection of seasonal anomalies

## 🔒 Security

- Isolated Docker network (soc_network)
- No external port exposure except frontend
- Internal service-to-service communication
- Environment-based configuration

## 📝 Environment Variables

Configuration via docker-compose.yml (customizable):

```yaml
ELASTICSEARCH_URL: http://elasticsearch:9200
CLICKHOUSE_URL: clickhouse:9000
REDIS_URL: redis://redis:6379
```

## 🐛 Troubleshooting

```bash
# View service status
docker-compose ps

# Check specific service logs
docker-compose logs backend

# Restart services
docker-compose restart

# Clean up and rebuild
docker-compose down -v
docker-compose up --build -d
```

## 📚 API Documentation

Endpoints will be available at `http://localhost:20006/api/`

## 🤝 Contributing

Contributions welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

MIT License - see LICENSE file for details

## 👤 Author

eentost - [GitHub](https://github.com/eentost)

## 🙏 Acknowledgments

- Elasticsearch community
- ClickHouse project
- Go ecosystem
- React community
