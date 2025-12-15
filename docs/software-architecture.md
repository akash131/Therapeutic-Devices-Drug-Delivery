# Software Architecture

Comprehensive software architecture documentation for therapeutic medical devices, covering embedded systems, mobile applications, cloud platforms, and enterprise integrations.

## Embedded Software Architecture

### Layered Architecture Model
```
┌─────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                         │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐           │
│  │   Therapy   │ │    User     │ │   Data      │           │
│  │   Engine    │ │  Interface  │ │   Logging   │           │
│  └─────────────┘ └─────────────┘ └─────────────┘           │
├─────────────────────────────────────────────────────────────┤
│                    MIDDLEWARE LAYER                          │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐           │
│  │   Safety    │ │   Comm      │ │   Device    │           │
│  │   Monitor   │ │   Stack     │ │   Drivers   │           │
│  └─────────────┘ └─────────────┘ └─────────────┘           │
├─────────────────────────────────────────────────────────────┤
│                    OS/RTOS LAYER                            │
│  ┌─────────────────────────────────────────────────────┐   │
│  │   FreeRTOS / QNX / VxWorks / ThreadX / Zephyr       │   │
│  └─────────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────────┤
│                    HAL/BSP LAYER                            │
│  ┌─────────────────────────────────────────────────────┐   │
│  │   Hardware Abstraction Layer / Board Support Package │   │
│  └─────────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────────┤
│                    HARDWARE LAYER                           │
│  ┌─────────────────────────────────────────────────────┐   │
│  │   MCU / Sensors / Actuators / Communication         │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### Safety-Critical Architecture

#### Dual-Processor Design
```
┌──────────────────────────────────────────────────────────────┐
│                    DUAL PROCESSOR ARCHITECTURE                │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────────────────┐    ┌──────────────────────┐       │
│  │   APPLICATION CPU    │    │    SAFETY CPU        │       │
│  │                      │    │                      │       │
│  │  ┌────────────────┐  │    │  ┌────────────────┐  │       │
│  │  │ User Interface │  │    │  │ Safety Monitor │  │       │
│  │  │ Data Management│  │    │  │ Watchdog       │  │       │
│  │  │ Communication  │  │    │  │ Limit Checking │  │       │
│  │  │ Non-Critical   │  │    │  │ Redundant Calc │  │       │
│  │  └────────────────┘  │    │  └────────────────┘  │       │
│  │                      │    │                      │       │
│  │  OS: Linux/RTOS     │    │  OS: Bare-metal/RTOS │       │
│  └──────────┬───────────┘    └──────────┬───────────┘       │
│             │                           │                    │
│             │    ┌──────────────┐      │                    │
│             └───►│   Shared     │◄─────┘                    │
│                  │   Memory     │                            │
│                  │   Heartbeat  │                            │
│                  └──────┬───────┘                            │
│                         │                                    │
│              ┌──────────▼──────────┐                        │
│              │   Output Control     │                        │
│              │   (Therapy Delivery) │                        │
│              └─────────────────────┘                        │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

#### IEC 62304 Software Classes

| Class | Risk Level | Documentation Required |
|-------|------------|------------------------|
| **A** | No injury possible | Development plan, requirements, architecture |
| **B** | Non-serious injury possible | + Detailed design, unit testing, integration testing |
| **C** | Death/serious injury possible | + Traceability, code review, static analysis |

### RTOS Implementation

#### Task Architecture
```c
/* Typical Medical Device Task Structure */

/* High Priority - Safety Critical */
Task: Safety_Monitor (Priority: Highest)
├── Period: 1ms
├── Deadline: Hard
├── Functions:
│   ├── Hardware fault detection
│   ├── Limit checking
│   ├── Watchdog servicing
│   └── Emergency shutdown
└── Stack: 1KB

/* High Priority - Therapy Delivery */
Task: Therapy_Control (Priority: High)
├── Period: 10ms
├── Deadline: Hard
├── Functions:
│   ├── Algorithm execution
│   ├── Output calculation
│   ├── Closed-loop control
│   └── Sensor processing
└── Stack: 2KB

/* Medium Priority - User Interface */
Task: UI_Handler (Priority: Medium)
├── Period: 50ms
├── Deadline: Soft
├── Functions:
│   ├── Display update
│   ├── Button/touch processing
│   ├── Menu navigation
│   └── Alert presentation
└── Stack: 4KB

/* Low Priority - Communication */
Task: Comm_Handler (Priority: Low)
├── Period: 100ms
├── Deadline: Soft
├── Functions:
│   ├── Bluetooth processing
│   ├── Data transmission
│   ├── Protocol handling
│   └── Buffer management
└── Stack: 4KB

/* Background - Data Logging */
Task: Data_Logger (Priority: Lowest)
├── Period: 1000ms
├── Deadline: None
├── Functions:
│   ├── Event logging
│   ├── Flash storage
│   ├── History management
│   └── Data compression
└── Stack: 2KB
```

#### Inter-Task Communication
```
Communication Mechanisms:
├── Message Queues
│   ├── Sensor data to processing
│   ├── Commands to therapy engine
│   └── Events to logger
├── Semaphores
│   ├── Resource protection
│   ├── Task synchronization
│   └── Critical section entry
├── Event Flags
│   ├── Alarm conditions
│   ├── State changes
│   └── Interrupt notifications
└── Shared Memory
    ├── Real-time parameters
    ├── Status registers
    └── Configuration data
```

---

## Therapy Algorithms

### Closed-Loop Control Systems

#### Insulin Delivery Algorithm (AID)
```
┌─────────────────────────────────────────────────────────────┐
│              AUTOMATED INSULIN DELIVERY                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  INPUT SIGNALS:                                             │
│  ├── CGM glucose value (mg/dL)                             │
│  ├── Glucose rate of change (mg/dL/min)                    │
│  ├── Insulin-on-board (IOB)                                │
│  ├── Carbohydrate input (optional)                         │
│  └── Exercise/activity state                                │
│                                                             │
│  ALGORITHM COMPONENTS:                                       │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Model Predictive Control (MPC) or PID Controller   │   │
│  │  ┌─────────────────────────────────────────────┐   │   │
│  │  │  Glucose Prediction Model                    │   │   │
│  │  │  ├── Insulin pharmacokinetics               │   │   │
│  │  │  ├── Carbohydrate absorption                │   │   │
│  │  │  └── Individual parameters                  │   │   │
│  │  └─────────────────────────────────────────────┘   │   │
│  │  ┌─────────────────────────────────────────────┐   │   │
│  │  │  Safety Constraints                          │   │   │
│  │  │  ├── Maximum delivery limits                │   │   │
│  │  │  ├── Hypoglycemia prevention               │   │   │
│  │  │  └── IOB limits                            │   │   │
│  │  └─────────────────────────────────────────────┘   │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  OUTPUT:                                                    │
│  ├── Basal rate adjustment (0-200% or absolute)            │
│  ├── Auto-bolus (micro-boluses)                            │
│  └── Suspend delivery (if predicted hypo)                  │
│                                                             │
│  CONTROL LOOP: Every 5 minutes                             │
└─────────────────────────────────────────────────────────────┘
```

#### Adaptive DBS Algorithm
```
Closed-Loop Neurostimulation:

INPUT SIGNALS:
├── Local Field Potentials (LFP)
│   ├── Beta band power (13-30 Hz) for Parkinson's
│   ├── Gamma oscillations
│   └── Evoked potentials
├── Accelerometer data (tremor detection)
└── Patient input (symptom diary)

ALGORITHM:
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  State Estimation:                                      │
│  ├── Signal filtering (bandpass, artifact rejection)   │
│  ├── Feature extraction (power, coherence)             │
│  └── State classification (on/off medication)          │
│                                                         │
│  Control Law:                                           │
│  ├── Proportional control (amplitude adjustment)       │
│  ├── Threshold-based (on/off switching)               │
│  └── Model-based (predictive adjustment)              │
│                                                         │
│  Safety Bounds:                                         │
│  ├── Maximum stimulation amplitude                     │
│  ├── Maximum duty cycle                                │
│  └── Rate of change limits                             │
│                                                         │
└─────────────────────────────────────────────────────────┘

OUTPUT:
├── Stimulation amplitude (0-5 mA)
├── Pulse width (60-450 μs)
├── Frequency (2-250 Hz)
└── Contact configuration
```

### Safety Algorithms

#### Infusion Pump Dose Checking
```python
# Dose Error Reduction System (DERS) Logic

class DrugLibrary:
    def __init__(self):
        self.drugs = {}  # Drug database

    def check_dose(self, drug_id, dose, concentration, patient_weight):
        drug = self.drugs[drug_id]

        # Calculate dose per kg if weight-based
        if drug.weight_based:
            dose_per_kg = dose / patient_weight
        else:
            dose_per_kg = None

        # Check against limits
        result = DoseCheckResult()

        # Hard limits (cannot override)
        if dose > drug.hard_max or dose < drug.hard_min:
            result.status = "HARD_LIMIT_EXCEEDED"
            result.allow_infusion = False
            return result

        # Soft limits (requires override)
        if dose > drug.soft_max or dose < drug.soft_min:
            result.status = "SOFT_LIMIT_EXCEEDED"
            result.allow_infusion = True  # With override
            result.requires_override = True
            return result

        # Within normal range
        result.status = "WITHIN_LIMITS"
        result.allow_infusion = True
        return result

# Additional safety checks
def additional_safety_checks(infusion):
    checks = []

    # Rate check
    if infusion.rate > infusion.max_rate:
        checks.append("RATE_EXCEEDED")

    # Concentration check
    if infusion.concentration not in infusion.allowed_concentrations:
        checks.append("INVALID_CONCENTRATION")

    # Duration check
    if infusion.duration > infusion.max_duration:
        checks.append("DURATION_EXCEEDED")

    # Drug interaction check
    checks.extend(check_interactions(infusion.drug, active_infusions))

    return checks
```

---

## Mobile Application Architecture

### Cross-Platform Architecture
```
┌─────────────────────────────────────────────────────────────┐
│              COMPANION APP ARCHITECTURE                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  PRESENTATION LAYER:                                        │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  ├── React Native / Flutter / Native (Swift/Kotlin)│   │
│  │  ├── UI Components                                  │   │
│  │  ├── Screen Navigation                              │   │
│  │  └── Accessibility Support                          │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  BUSINESS LOGIC LAYER:                                      │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  ├── Device Communication Manager                   │   │
│  │  ├── Data Processing Engine                         │   │
│  │  ├── Alert/Notification Handler                     │   │
│  │  ├── User Authentication                            │   │
│  │  └── Analytics Engine                               │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  DATA LAYER:                                                │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  ├── Local Database (SQLite/Realm)                  │   │
│  │  ├── Secure Storage (Keychain/Keystore)            │   │
│  │  ├── Cache Manager                                  │   │
│  │  └── Sync Engine                                    │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  PLATFORM SERVICES:                                         │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  ├── Bluetooth LE Manager                           │   │
│  │  ├── HealthKit/Google Fit Integration              │   │
│  │  ├── Push Notification Service                      │   │
│  │  ├── Background Processing                          │   │
│  │  └── Biometric Authentication                       │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### BLE Communication Stack
```
┌─────────────────────────────────────────────────────────────┐
│                BLE PROTOCOL STACK                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  APPLICATION PROTOCOL:                                       │
│  ├── Custom GATT Services                                   │
│  │   ├── Device Information Service (0x180A)               │
│  │   ├── Battery Service (0x180F)                          │
│  │   ├── Glucose Service (0x1808)                          │
│  │   └── Custom Therapy Service (proprietary UUID)         │
│  └── Command/Response Protocol                              │
│      ├── Message framing                                    │
│      ├── Sequence numbering                                 │
│      ├── Acknowledgment                                     │
│      └── Error handling                                     │
│                                                             │
│  SECURITY LAYER:                                            │
│  ├── Pairing: LE Secure Connections (LESC)                 │
│  ├── Bonding: Long-term key storage                        │
│  ├── Encryption: AES-CCM (128-bit)                         │
│  └── Privacy: Resolvable Private Address (RPA)             │
│                                                             │
│  CONNECTION MANAGEMENT:                                      │
│  ├── Scanning/Discovery                                     │
│  ├── Connection parameters                                  │
│  │   ├── Interval: 15-30ms (interactive)                   │
│  │   ├── Interval: 100-500ms (background)                  │
│  │   └── Latency: Slave latency for power saving          │
│  └── Reconnection handling                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Data Security Implementation
```
Security Architecture:

ENCRYPTION:
├── Data at Rest
│   ├── AES-256 encryption for databases
│   ├── Secure enclave for keys (iOS)
│   ├── Android Keystore (Android)
│   └── Per-file encryption
├── Data in Transit
│   ├── TLS 1.3 for cloud communication
│   ├── BLE encryption (AES-CCM)
│   └── Certificate pinning
└── Data Processing
    ├── Memory encryption
    ├── Secure memory clearing
    └── Anti-debugging measures

AUTHENTICATION:
├── User Authentication
│   ├── Password + biometric
│   ├── Multi-factor authentication
│   └── Session management
├── Device Authentication
│   ├── Certificate-based
│   ├── Mutual authentication
│   └── Device binding
└── API Authentication
    ├── OAuth 2.0 + PKCE
    ├── JWT tokens (short-lived)
    └── Refresh token rotation

PRIVACY:
├── Data minimization
├── Anonymization for analytics
├── Consent management
├── HIPAA compliance
└── GDPR compliance
```

---

## Cloud Platform Architecture

### Healthcare Cloud Architecture
```
┌─────────────────────────────────────────────────────────────┐
│              CLOUD PLATFORM ARCHITECTURE                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              API GATEWAY / LOAD BALANCER             │   │
│  │  ├── Rate limiting                                   │   │
│  │  ├── Authentication                                  │   │
│  │  └── Request routing                                 │   │
│  └────────────────────────┬────────────────────────────┘   │
│                           │                                 │
│  ┌────────────────────────▼────────────────────────────┐   │
│  │              MICROSERVICES LAYER                     │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ │   │
│  │  │ Device   │ │ Patient  │ │Analytics │ │ Alert  │ │   │
│  │  │ Service  │ │ Service  │ │ Service  │ │Service │ │   │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────┘ │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ │   │
│  │  │ Auth     │ │ Report   │ │ Notif.   │ │ FHIR   │ │   │
│  │  │ Service  │ │ Service  │ │ Service  │ │Service │ │   │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────┘ │   │
│  └────────────────────────┬────────────────────────────┘   │
│                           │                                 │
│  ┌────────────────────────▼────────────────────────────┐   │
│  │              DATA LAYER                              │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ │   │
│  │  │PostgreSQL│ │  Redis   │ │  S3/Blob │ │Elastic │ │   │
│  │  │(Primary) │ │ (Cache)  │ │ (Files)  │ │(Search)│ │   │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────┘ │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              INFRASTRUCTURE                          │   │
│  │  ├── Kubernetes (Container orchestration)           │   │
│  │  ├── Terraform (Infrastructure as Code)             │   │
│  │  ├── Vault (Secrets management)                     │   │
│  │  └── Monitoring (Prometheus, Grafana)               │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Data Pipeline
```
Data Flow Architecture:

INGESTION:
├── Device Data Stream
│   ├── MQTT for real-time telemetry
│   ├── REST API for batch uploads
│   └── WebSocket for bidirectional
├── Message Queue
│   ├── Apache Kafka / AWS Kinesis
│   ├── Partitioning by device ID
│   └── Data retention (7-30 days)
└── Validation
    ├── Schema validation
    ├── Range checking
    ├── Timestamp verification
    └── Duplicate detection

PROCESSING:
├── Stream Processing
│   ├── Apache Flink / Spark Streaming
│   ├── Real-time analytics
│   ├── Alert detection
│   └── Aggregations
├── Batch Processing
│   ├── Daily summaries
│   ├── Trend analysis
│   └── Report generation
└── ML Pipeline
    ├── Feature engineering
    ├── Model inference
    └── Prediction serving

STORAGE:
├── Hot Storage (Recent data)
│   ├── Time-series DB (InfluxDB/TimescaleDB)
│   └── Fast query access
├── Warm Storage (Historical)
│   ├── Data warehouse
│   └── Analytics queries
└── Cold Storage (Archive)
    ├── Object storage (S3)
    ├── Compliance retention
    └── Cost optimization
```

### FHIR API Implementation
```
FHIR Server Configuration:

RESOURCES SUPPORTED:
├── Patient
├── Device
├── Observation
├── DiagnosticReport
├── MedicationAdministration
├── CarePlan
└── Practitioner

API ENDPOINTS:
├── CRUD Operations
│   ├── POST /fhir/Observation (Create)
│   ├── GET /fhir/Observation/:id (Read)
│   ├── PUT /fhir/Observation/:id (Update)
│   └── DELETE /fhir/Observation/:id (Delete)
├── Search
│   ├── GET /fhir/Observation?patient=123
│   ├── GET /fhir/Observation?date=gt2024-01-01
│   └── GET /fhir/Observation?code=glucose
├── Bulk Operations
│   ├── POST /fhir/$export (Bulk export)
│   └── POST /fhir (Batch/Transaction)
└── Subscriptions
    ├── POST /fhir/Subscription
    └── WebSocket/REST hook notifications

SMART ON FHIR:
├── OAuth 2.0 Authorization
├── Launch context
├── Scopes (patient/*.read, etc.)
└── App registration
```

---

## Testing Architecture

### Test Pyramid
```
Testing Strategy:

                    ┌─────────────┐
                    │   E2E/UI    │  (10%)
                    │   Tests     │
                   ┌┴─────────────┴┐
                   │  Integration  │  (20%)
                   │    Tests      │
                  ┌┴───────────────┴┐
                  │   Unit Tests    │  (70%)
                  └─────────────────┘

UNIT TESTING:
├── Framework: GoogleTest, Unity (embedded)
├── Coverage target: >80%
├── Mocking: Hardware abstraction
└── CI/CD: Every commit

INTEGRATION TESTING:
├── Hardware-in-loop (HIL)
├── Software-in-loop (SIL)
├── Communication protocols
└── Database interactions

SYSTEM TESTING:
├── Functional testing
├── Performance testing
├── Stress testing
├── Endurance testing
└── Recovery testing

VERIFICATION & VALIDATION:
├── Requirements traceability
├── Risk-based testing
├── Usability testing
└── Clinical validation
```

### Automated Testing Framework
```
CI/CD Pipeline:

CONTINUOUS INTEGRATION:
├── Code Commit
│   ├── Static analysis (SonarQube, Coverity)
│   ├── Unit tests
│   └── Code coverage
├── Build
│   ├── Cross-compilation (ARM targets)
│   ├── Dependency management
│   └── Binary signing
└── Automated Tests
    ├── Integration tests
    ├── Simulation tests
    └── Regression tests

CONTINUOUS DEPLOYMENT:
├── Staging Environment
│   ├── Deploy to test devices
│   ├── Automated functional tests
│   └── Performance benchmarks
├── Validation
│   ├── Manual verification
│   ├── Security scan
│   └── Compliance check
└── Release
    ├── Version tagging
    ├── Release notes
    ├── Documentation update
    └── Regulatory submission (if required)
```

---

## DevOps and Deployment

### Medical Device DevOps
```
DevOps Practices for Medical Devices:

SOURCE CONTROL:
├── Git with signed commits
├── Branch protection
├── Code review requirements
└── Audit trail preservation

BUILD SYSTEM:
├── Reproducible builds
├── Build artifact versioning
├── Dependency management
├── SBOM generation

DEPLOYMENT:
├── Blue-green deployment (cloud)
├── Canary releases (mobile apps)
├── Staged rollout (firmware)
└── Rollback capability

MONITORING:
├── Application performance
├── Error tracking (Sentry, Crashlytics)
├── Usage analytics
├── Compliance monitoring

DOCUMENTATION:
├── Auto-generated API docs
├── Architecture diagrams as code
├── Change control integration
└── Regulatory document generation
```

### Firmware Update System
```
Over-the-Air (OTA) Update Architecture:

UPDATE PACKAGE:
├── Firmware binary (signed)
├── Version manifest
├── Cryptographic signatures
├── Rollback image
└── Update instructions

UPDATE PROCESS:
1. Check for updates
   ├── Periodic polling
   └── Push notification

2. Download package
   ├── Background download
   ├── Resume capability
   └── Integrity verification

3. Validate package
   ├── Signature verification
   ├── Version compatibility
   ├── Dependency checking
   └── Size verification

4. Install update
   ├── Dual-bank switching
   ├── Bootloader validation
   └── Configuration migration

5. Verify installation
   ├── Self-test
   ├── Checksum verification
   └── Functional validation

6. Report status
   ├── Success/failure notification
   └── Telemetry logging

ROLLBACK:
├── Automatic on boot failure
├── Manual trigger option
├── Previous version retention
└── Configuration preservation
```

---

## Compliance and Documentation

### IEC 62304 Compliance
```
Software Development Lifecycle:

PLANNING:
├── Software Development Plan
├── Configuration Management Plan
├── Risk Management Plan
└── Quality Assurance Plan

REQUIREMENTS:
├── Software Requirements Specification (SRS)
├── Traceability matrix
├── Risk analysis integration
└── Requirements review

ARCHITECTURE:
├── Software Architecture Description
├── Interface specifications
├── Security architecture
└── SOUP identification

DETAILED DESIGN:
├── Module specifications
├── Algorithm descriptions
├── Data structures
└── Design patterns

IMPLEMENTATION:
├── Coding standards compliance
├── Code review process
├── Static analysis
└── Unit testing

VERIFICATION:
├── Integration testing
├── System testing
├── Acceptance testing
└── Regression testing

RELEASE:
├── Release notes
├── Known anomalies
├── Installation instructions
└── User documentation

MAINTENANCE:
├── Problem reports
├── Change requests
├── Impact analysis
└── Regression testing
```

### Traceability Matrix
```
Requirement → Design → Code → Test Mapping:

┌─────────────┬──────────────┬─────────────┬─────────────┐
│ Requirement │ Design Spec  │ Source File │ Test Case   │
├─────────────┼──────────────┼─────────────┼─────────────┤
│ SRS-001     │ SAD-2.1      │ therapy.c   │ TC-001,002  │
│ SRS-002     │ SAD-2.2      │ safety.c    │ TC-010-015  │
│ SRS-003     │ SAD-3.1      │ comm.c      │ TC-020-025  │
└─────────────┴──────────────┴─────────────┴─────────────┘

Bidirectional Traceability:
├── Forward: Requirement → Implementation
├── Backward: Code → Requirement
├── Coverage analysis
└── Gap identification
```
