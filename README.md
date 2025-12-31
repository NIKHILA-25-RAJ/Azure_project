# Cryptocurrency Data Pipeline Architecture

## Overview

This repository contains the architecture and documentation for a real-time cryptocurrency data pipeline built on Microsoft Azure. The system ingests, processes, and analyzes cryptocurrency market data using a modern medallion architecture, enabling comprehensive market analysis, trading insights, and portfolio monitoring.

# Architecture Flow

External API
     ↓
Azure Data Factory (Ingestion & Orchestration)
     ↓
Azure Data Lake Storage
   ├─ Raw Layer
   ├─ Ingestion Layer
   └─ Presentation Layer
     ↓
Databricks / Transform Logic
     ↓
Power BI (Analytics & Visualization)   

## Architecture Components

### 1. Data Ingestion Layer

**API Integration**
- External data sources are consumed through API endpoints
- Raw data is collected from various sources in its original format
- Initial entry point for all data flowing into the system

**Azure Data Factory (ADF)**
- Orchestrates the entire data movement and transformation workflow
- Schedules and monitors data pipeline executions
- Provides connectivity between different components
- Handles error handling and retry logic

### 2. Storage Architecture 

The architecture implements a three-layer medallion structure using Azure Data Lake Storage:

#### Raw Layer (Bronze)
- **Purpose**: Store raw, unprocessed data exactly as received from source systems
- **Characteristics**:
  - Immutable data storage
  - Preserves original data lineage
  - No transformations applied
  - Supports data recovery and reprocessing

#### Ingestion Layer (Silver)
- **Purpose**: Cleaned and conformed data ready for transformation
- **Characteristics**:
  - Data quality checks applied
  - Standardized formats and schemas
  - Duplicate removal
  - Basic data cleansing operations

#### Presentation Layer (Gold)
- **Purpose**: Business-ready, aggregated data optimized for consumption
- **Characteristics**:
  - Aggregated metrics and KPIs
  - Denormalized for query performance
  - Business logic applied
  - Ready for analytics and reporting

### 3. Data Processing Stages

**Ingest**
- Raw data extraction from APIs
- Initial data validation
- Storage in Raw Layer

**Transform**
- Data cleansing and standardization
- Schema evolution handling
- Business rule application
- Data enrichment
  
### 4. Orchestration

**Azure Data Factory**
- Centralized orchestration of all pipeline activities
- Manages dependencies between pipeline stages
- Implements scheduling and triggering mechanisms
- Provides monitoring and alerting capabilities
- Enables CI/CD for pipeline deployments

### 5. Visualization Layer

**Power BI**
- Connects to Presentation Layer (Gold)
- Creates interactive dashboards and reports
- Provides self-service analytics capabilities
- Enables data exploration and insights discovery
- Supports scheduled refresh from data lake

**Visualization Outputs**

Pie Chart: Portfolio distribution by cryptocurrency showing percentage allocation
Charge Analysis: Sum of transaction charges by token name
Color-coded Legend: Easy identification of each cryptocurrency position


## Data Flow

 **API → Azure Data Factory**: External data sources send data through APIs
 **ADF → Raw Layer**: Unprocessed data lands in Data Lake Storage (Bronze)
 **Raw → Ingestion Layer**: Data is cleaned and standardized (Silver)
 **Ingestion → Presentation Layer**: Data is transformed and aggregated (Gold)
 **Presentation → Analysis**: Advanced analytics and statistical processing
 **Presentation → Power BI**: Business intelligence and visualization
 **Feedback Loop**: ADF orchestrates the entire process and manages reprocessing

## Key Benefits

### Scalability
- Cloud-native architecture scales horizontally
- Handle growing data volumes seamlessly
- Pay-as-you-go pricing model

### Data Quality
- Multi-layer validation and cleansing
- Audit trail maintained across all layers
- Easy data recovery and reprocessing

### Flexibility
- Support for various data sources and formats
- Adaptable transformation logic
- Extensible architecture for new requirements

### Performance
- Optimized storage in presentation layer
- Distributed processing capabilities
- Efficient query performance

## Technology Stack

- **Cloud Platform**: Microsoft Azure
- **Orchestration**: Azure Data Factory
- **Storage**: Azure Data Lake Storage Gen2
- **Visualization**: Microsoft Power BI
- **Data Processing**: Azure Databricks / Azure Synapse Analytics (implied)

## Best Practices Implemented

1. **Immutable Raw Data**: Original data is never modified
2. **Incremental Processing**: Only new or changed data is processed
3. **Schema Evolution**: Handle changes in source data structure
4. **Error Handling**: Comprehensive logging and retry mechanisms
5. **Security**: Role-based access control across layers
6. **Monitoring**: End-to-end pipeline monitoring and alerting

### Prerequisites
- Azure subscription
- Azure Data Factory instance
- Azure Data Lake Storage Gen2 account
- Power BI workspace
- Appropriate IAM permissions

### Setup Steps
1. Configure Azure Data Factory connections
2. Set up Data Lake Storage containers (raw, ingestion, presentation)
3. Deploy pipeline definitions
4. Configure source API connections
5. Set up Power BI datasets and reports
6. Schedule pipeline triggers

## Monitoring and Maintenance

- Monitor pipeline runs through Azure Data Factory portal
- Set up alerts for pipeline failures
- Review data quality metrics regularly
- Maintain documentation for transformations
- Implement version control for pipeline code


