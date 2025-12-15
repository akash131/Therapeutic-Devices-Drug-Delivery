# Regulatory Compliance Guide

Comprehensive guide to regulatory requirements, standards, and compliance pathways for therapeutic medical devices across global markets.

## Regulatory Frameworks by Region

### United States - FDA

#### Device Classification
| Class | Risk | Regulatory Control | Examples |
|-------|------|-------------------|----------|
| Class I | Low | General controls | Bandages, examination gloves |
| Class II | Moderate | General + Special controls | Infusion pumps, TENS units |
| Class III | High | General + Premarket approval | Pacemakers, implantable pumps |

#### Premarket Pathways

##### 510(k) Premarket Notification
```
Requirements:
├── Substantial equivalence to predicate device
├── Intended use comparison
├── Technological characteristics
├── Performance testing (as needed)
└── Labeling

Timeline: 3-6 months (typical)
Fee: ~$21,000 (small business: ~$5,000)
```

##### Premarket Approval (PMA)
```
Requirements:
├── Valid scientific evidence of safety/efficacy
├── Clinical trials (usually required)
├── Manufacturing quality system
├── Labeling and promotional materials
├── Post-approval requirements

Timeline: 12-18 months (typical)
Fee: ~$420,000 (small business: ~$105,000)
```

##### De Novo Classification
```
For novel devices without predicate:
├── Risk determination
├── General/special controls identification
├── Performance data
├── Creates new classification

Timeline: 6-12 months
Fee: ~$130,000 (small business: ~$32,500)
```

##### Breakthrough Device Designation
```
Benefits:
├── Interactive FDA communication
├── Priority review
├── Senior management involvement
├── Reduced clinical data (risk-based)

Criteria:
├── More effective diagnosis/treatment
├── Breakthrough technology
├── Significant advantages
└── Life-threatening/irreversibly debilitating condition
```

#### Quality System Regulation (QSR)
21 CFR Part 820 requirements:
- Design controls
- Document controls
- Purchasing controls
- Production and process controls
- Corrective and preventive action (CAPA)
- Device master record
- Device history record

#### Unique Device Identification (UDI)
```
UDI Components:
├── Device Identifier (DI)
│   ├── Labeler identification
│   └── Product model
├── Production Identifier (PI)
│   ├── Lot/batch number
│   ├── Serial number
│   ├── Manufacturing date
│   └── Expiration date
└── GUDID Database Registration
```

---

### European Union - MDR

#### Medical Device Regulation (EU 2017/745)
Replaced MDD (93/42/EEC) with stricter requirements.

##### Classification Rules
| Class | Risk | Examples |
|-------|------|----------|
| Class I | Low | Non-sterile, non-measuring |
| Class Is | Low (sterile) | Sterile gloves |
| Class Im | Low (measuring) | Thermometers |
| Class IIa | Medium-low | Infusion pumps, hearing aids |
| Class IIb | Medium-high | Ventilators, implantable sutures |
| Class III | High | Pacemakers, hip implants |

##### Conformity Assessment
```
Class I: Self-declaration (Annex II-III)
Class Is/Im: Notified body for specific aspects
Class IIa: Notified body (Annex IX or XI + X)
Class IIb: Notified body (Annex IX or X + XI)
Class III: Notified body (Annex IX + X clinical evaluation)
```

##### Technical Documentation Requirements
- Device description and specification
- Design and manufacturing information
- General safety and performance requirements
- Benefit-risk analysis
- Product verification and validation
- Clinical evaluation
- Post-market surveillance plan

##### EUDAMED Database
```
Modules:
├── Actor registration
├── UDI/Device registration
├── Notified body certificates
├── Clinical investigations
├── Vigilance reporting
└── Market surveillance
```

##### Clinical Evaluation
```
Clinical Evidence Sources:
├── Clinical investigations
├── Published literature
├── Clinical experience (post-market)
└── Equivalent device data (restricted)

Clinical Evaluation Report (CER):
├── Device description
├── Clinical background
├── State of the art
├── Data sources and appraisal
├── Clinical data analysis
├── Conclusions
└── Update schedule (annual minimum)
```

---

### Other Key Markets

#### Japan - PMDA
```
Classification:
├── Class I: General medical devices (notification)
├── Class II: Controlled medical devices (certification)
├── Class III: Specially controlled (PMDA review)
└── Class IV: Highly controlled (PMDA review)

Pathway: Shonin (approval) required for Class III-IV
Foreign Manufacturer: QMS certification required
```

#### China - NMPA
```
Classification:
├── Class I: Filing only
├── Class II: Provincial approval
└── Class III: NMPA approval

Requirements:
├── China clinical trials (often required)
├── In-country testing
├── Chinese-language labeling
└── China representative
```

#### Brazil - ANVISA
```
Classification:
├── Class I: Registration
├── Class II: Registration
├── Class III: Registration with technical report
└── Class IV: Registration with clinical data

Good Manufacturing: GMP certificate required
```

#### Canada - Health Canada
```
Classification:
├── Class I: Establishment license only
├── Class II: Device license (declaration)
├── Class III: Device license (review)
└── Class IV: Device license (detailed review)

Quality System: ISO 13485 recognition
```

---

## Essential Standards

### Quality Management

#### ISO 13485:2016
Medical devices quality management system.
```
Key Requirements:
├── Context and leadership
├── Planning
├── Support (resources, competence)
├── Operations
│   ├── Design and development
│   ├── Purchasing
│   ├── Production
│   └── Control of monitoring equipment
├── Performance evaluation
└── Improvement
```

#### 21 CFR Part 820 (US QSR)
FDA quality system requirements (harmonizing with ISO 13485).

### Safety and Performance

#### IEC 60601-1 (General Safety)
Medical electrical equipment - General requirements.
```
Key Sections:
├── General requirements
├── Environmental conditions
├── Protection against electrical hazards
├── Protection against mechanical hazards
├── Protection against unwanted radiation
├── Protection against excessive temperatures
├── Accuracy of controls
├── Hazardous situations
├── Programmable electrical systems (PEMS)
├── Construction
└── Marking and documents
```

#### IEC 60601-1-2 (EMC)
Electromagnetic compatibility requirements.
```
Immunity Requirements:
├── Electrostatic discharge (ESD)
├── Radiated RF electromagnetic fields
├── Electrical fast transients (EFT)
├── Surges
├── Conducted RF disturbances
├── Power frequency magnetic fields
├── Voltage dips and interruptions
└── Proximity fields from wireless equipment
```

#### IEC 60601-1-6 (Usability)
Usability engineering process.

#### IEC 60601-1-8 (Alarms)
Alarm systems requirements.
```
Alarm Categories:
├── High priority: Immediate response required
├── Medium priority: Prompt response required
└── Low priority: Awareness required

Signal Requirements:
├── Auditory characteristics
├── Visual characteristics
├── Distributed alarm systems
└── Alarm condition delays
```

### Device-Specific Standards

| Device Type | Key Standards |
|-------------|---------------|
| Infusion pumps | IEC 60601-2-24 |
| Pacemakers | ISO 14708-2 |
| ICDs | ISO 14708-6 |
| Cochlear implants | ISO 14708-7 |
| Neurostimulators | ISO 14708-3 |
| Insulin pumps | IEC 60601-2-24, ISO 11608 |
| Surgical robots | IEC 80601-2-77 |
| Ventilators | ISO 80601-2-12 |
| Nebulizers | ISO 27427 |

### Software Standards

#### IEC 62304 (Software Lifecycle)
```
Software Safety Classification:
├── Class A: No injury or damage to health possible
├── Class B: Non-serious injury possible
└── Class C: Death or serious injury possible

Required Activities by Class:
| Activity | Class A | Class B | Class C |
|----------|---------|---------|---------|
| Development planning | ✓ | ✓ | ✓ |
| Requirements analysis | ✓ | ✓ | ✓ |
| Architecture design | - | ✓ | ✓ |
| Detailed design | - | - | ✓ |
| Unit implementation | ✓ | ✓ | ✓ |
| Integration testing | ✓ | ✓ | ✓ |
| System testing | ✓ | ✓ | ✓ |
```

#### IEC 62443 (Cybersecurity)
Industrial automation and control systems security.

#### FDA Cybersecurity Guidance
```
Premarket Considerations:
├── Security risk management
├── Security architecture
├── Cybersecurity testing
├── Labeling (SBOM, security info)
└── Documentation

Postmarket Considerations:
├── Vulnerability monitoring
├── Coordinated disclosure
├── Patching/updates
├── Customer communication
└── Incident response
```

### Risk Management

#### ISO 14971:2019
Application of risk management to medical devices.
```
Risk Management Process:
├── Risk analysis
│   ├── Intended use identification
│   ├── Hazard identification
│   ├── Risk estimation
│   └── Documentation
├── Risk evaluation
│   ├── Acceptability criteria
│   ├── Risk/benefit analysis
│   └── Priority determination
├── Risk control
│   ├── Option analysis
│   ├── Implementation
│   ├── Residual risk evaluation
│   └── Benefit-risk review
├── Overall residual risk
└── Risk management report
```

### Biocompatibility

#### ISO 10993 Series
Biological evaluation of medical devices.
```
Part 1: Evaluation framework
├── Device categorization
│   ├── Contact nature (surface, external, implant)
│   ├── Contact duration (<24h, 24h-30d, >30d)
│   └── Contact type (skin, tissue, blood)
├── Endpoint selection
│   ├── Cytotoxicity
│   ├── Sensitization
│   ├── Irritation
│   ├── Systemic toxicity
│   ├── Genotoxicity
│   ├── Implantation
│   ├── Hemocompatibility
│   └── Others as applicable
└── Testing strategy
```

---

## Clinical Evaluation

### Clinical Investigation Requirements

#### IDE (Investigational Device Exemption) - US
```
Significant Risk Devices:
├── FDA IDE approval required
├── IRB approval
├── Informed consent
├── Monitoring requirements
├── Adverse event reporting
└── Records and reports

Non-Significant Risk Devices:
├── IRB approval only
├── Abbreviated requirements
└── Sponsor determination
```

#### Clinical Investigation - EU MDR
```
Article 62-82 Requirements:
├── Scientific validity
├── Ethics committee approval
├── Member state authorization
├── EUDAMED registration
├── Informed consent
├── Sponsor responsibilities
└── Safety reporting (SAE within 7 days)
```

### Clinical Evidence Requirements

#### MEDDEV 2.7/1 Rev 4 Guidelines
```
Clinical Evaluation Process:
Stage 0: Scoping
├── Device description
├── Intended purpose
├── GSPR applicability

Stage 1: Identification
├── Literature search
├── Clinical data sources
├── Equivalence assessment

Stage 2: Appraisal
├── Data relevance
├── Data quality
├── Weighting methodology

Stage 3: Analysis
├── Safety analysis
├── Performance analysis
├── Benefit-risk determination

Stage 4: Report
├── Clinical Evaluation Report (CER)
├── Conclusions
├── Update plan (PMCF)
```

---

## Post-Market Requirements

### Vigilance and Reporting

#### US - MDR (Medical Device Reporting)
```
Reportable Events:
├── Deaths
├── Serious injuries
└── Malfunctions that could cause death/injury

Timelines:
├── 30 days: Standard reports
├── 5 days: Remedial action reports
└── 5 days: FDA requests
```

#### EU - Vigilance
```
Serious Incidents:
├── Death
├── Serious deterioration in health
├── Public health threat

Timelines:
├── 2 days: Serious public health threat
├── 10 days: Death or serious deterioration
├── 15 days: Other serious incidents
```

### Field Safety Actions

#### Recalls and Corrections
```
US Recall Classes:
├── Class I: Reasonable probability of serious health consequences or death
├── Class II: May cause temporary or reversible adverse health consequences
└── Class III: Not likely to cause adverse health consequences

EU Field Safety Corrective Actions (FSCA):
├── Device recall
├── Device modification
├── Device destruction
├── Exchange of device
└── Customer advice
```

### Post-Market Surveillance

#### PMS Requirements (EU MDR)
```
PMS Plan Contents:
├── Proactive collection methods
├── Reactive collection methods
├── Complaint handling
├── Trend analysis
├── Risk management updates
├── PMCF plan (if applicable)
└── PSUR schedule

Post-Market Clinical Follow-up (PMCF):
├── Objective and rationale
├── Methods (registry, survey, study)
├── Sample size justification
├── Analysis plan
└── Integration with CER
```

#### Periodic Safety Update Report (PSUR)
```
Contents:
├── Device identification
├── Safety data summary
├── Worldwide sales data
├── Benefit-risk conclusions
├── Ongoing studies
└── Proposed actions

Frequency:
├── Class IIa: When required or every 2 years
├── Class IIb: Annually
├── Class III: Annually
├── Implantables: Annually
```

---

## Cybersecurity Requirements

### FDA Cybersecurity Framework
```
Premarket Submission Requirements:
├── Threat modeling
├── Cybersecurity risk assessment
├── Security controls
├── Vulnerability testing
├── Software Bill of Materials (SBOM)
└── Update/patch mechanism

Postmarket Management:
├── Vulnerability monitoring
├── Coordinated disclosure policy
├── Incident response plan
├── Customer notification process
└── End-of-life planning
```

### IEC 81001-5-1 (Health Software Security)
```
Security Requirements:
├── Security risk management
├── Secure development lifecycle
├── Security testing
├── Vulnerability handling
├── Security maintenance
└── Security documentation
```

---

## Compliance Checklist

### Pre-Submission Checklist
```
☐ Device classification determined
☐ Predicate/equivalent device identified (if applicable)
☐ Standards list compiled
☐ Quality system certified/compliant
☐ Risk management file complete
☐ Design documentation complete
☐ Verification and validation complete
☐ Biocompatibility assessment done
☐ Clinical evaluation complete
☐ Labeling prepared
☐ Cybersecurity documentation ready
☐ UDI assigned
☐ Post-market surveillance plan drafted
```

### Post-Market Compliance Checklist
```
☐ Vigilance system operational
☐ Complaint handling process active
☐ PMS plan implemented
☐ CER updates scheduled
☐ PSUR schedule established
☐ Field safety procedures documented
☐ Supplier monitoring ongoing
☐ Quality metrics tracked
☐ Regulatory intelligence monitored
☐ Registration renewals calendared
```
