# Bharat Sahayak - Requirements Document

## 1. Project Overview

Bharat Sahayak is an AI-powered, voice-first solution designed to bridge the digital divide in rural India by enabling access to government welfare schemes through simple SMS and IVR technology. The platform eliminates the need for smartphones, internet connectivity, or digital literacy, making government benefits accessible to over 500 million rural Indians who own feature phones.

The system works through a simple three-step process: users send an SMS with a keyword to a designated number, receive an automated IVR callback within seconds, and engage in a natural language conversation in Hindi or their regional language. An AI-powered engine analyzes their responses, matches them with relevant government schemes from a database of 500+ programs, and sends personalized results via SMS with clear application steps.

By leveraging AWS cloud services including Amazon Bedrock, Amazon Connect, and Amazon Lex, Bharat Sahayak aims to unlock ₹1.47 lakh crore in unclaimed government benefits, reduce application time by 50%, and provide a cost-effective solution at less than ₹5 per user interaction—100 times cheaper than traditional Common Service Center visits.

## 2. Problem Statement

India faces a critical challenge in welfare delivery despite having numerous government schemes designed to support its citizens. Current statistics reveal the severity of this gap:

- 65% of government welfare schemes fail to reach their intended beneficiaries due to lack of awareness, complex application processes, and digital barriers
- ₹1.47 lakh crore (approximately $18 billion USD) in government benefits remains unclaimed annually
- Over 500 million rural Indians own feature phones but lack smartphone access or internet connectivity
- Traditional access points like Common Service Centers (CSCs) are expensive (₹500+ per visit), geographically distant, and require travel time and costs
- Low literacy rates (particularly digital literacy) create additional barriers to accessing online portals and mobile applications
- Language barriers persist as most government portals are primarily in English or Hindi, excluding speakers of regional languages
- Information asymmetry leaves eligible citizens unaware of schemes they qualify for

The absence of a simple, accessible, and inclusive solution perpetuates the cycle of poverty and prevents the government's welfare investments from reaching those who need them most.

## 3. Target Users

### Primary User Segments

1. Rural Indians with feature phones (500M+ population)
2. Low-literacy and digitally illiterate citizens
3. Senior citizens in rural and semi-urban areas
4. Agricultural workers and small-scale farmers
5. Women in rural households with limited mobility
6. Daily wage laborers and informal sector workers

### User Persona: Ramesh Kumar

- Age: 45 years old
- Location: Small village in Bihar
- Occupation: Small-scale farmer with 2 acres of land
- Family: Wife and three children (ages 12, 15, 18)
- Education: Completed primary school (Class 5)
- Technology: Owns a basic feature phone, no internet access
- Language: Speaks Hindi and Bhojpuri, limited English
- Income: ₹8,000-12,000 per month (seasonal)
- Challenges: Unaware of agricultural subsidies, crop insurance, and education schemes for children; nearest CSC is 15 km away; cannot afford smartphone or internet data
- Goals: Access government schemes for farm equipment subsidy, PM-KISAN benefits, and scholarships for children's education

## 4. Functional Requirements

### 4.1 SMS Trigger System

- User sends SMS with keyword "SCHEME" to designated short code or 10-digit number
- System captures user's mobile number automatically
- System validates mobile number format and telecom operator
- System initiates IVR callback workflow within 5 seconds
- System supports multiple trigger keywords (SCHEME, YOJANA, HELP, INFO)
- System handles SMS in English and Hindi (Devanagari script)
- System provides confirmation SMS acknowledging request received

### 4.2 Voice-First IVR Interface

- Automated callback to user's mobile number within 5 seconds of SMS trigger
- Natural language conversation in Hindi (primary) and regional languages
- Voice prompts guide user through information collection process
- System asks contextual questions about:
  - Age and family composition
  - Occupation and income level
  - Location (state, district, village)
  - Specific needs (health, education, agriculture, housing, etc.)
  - Existing government ID cards (Aadhaar, ration card, etc.)
- Support for voice input with pause detection and interruption handling
- Option to repeat questions or go back to previous question
- Graceful error handling for unclear responses
- Average call duration: 2-3 minutes
- Call recording for quality assurance (with user consent)

### 4.3 AI-Powered Scheme Matching

- Real-time analysis of user responses using Amazon Bedrock (Claude AI)
- Natural language understanding to extract key eligibility criteria
- Matching algorithm compares user profile against 500+ government schemes
- Ranking of schemes by relevance score (eligibility match percentage)
- Consideration of central, state, and district-level schemes
- Filtering based on:
  - Demographic criteria (age, gender, caste, disability status)
  - Economic criteria (income level, BPL status)
  - Geographic criteria (state, district, rural/urban)
  - Occupational criteria (farmer, laborer, artisan, etc.)
  - Special categories (women, senior citizens, students, etc.)
- Top 3-5 most relevant schemes selected for delivery
- Fallback to general schemes if no specific matches found

### 4.4 Results Delivery System

- SMS sent to user within 30 seconds of call completion
- SMS contains:
  - Names of matched schemes (in user's language)
  - Brief one-line description of each scheme
  - Eligibility confirmation
  - Application process overview
  - Required documents list
  - Contact information or helpline number
  - Unique reference ID for follow-up
- Multiple SMS messages if content exceeds 160 characters
- Option to receive detailed information via follow-up call
- SMS includes link to voice message (for users who prefer audio)
- Retry mechanism for failed SMS delivery

### 4.5 Multi-Language Support

- Hindi as primary language
- Support for 10+ Indian languages in phases:
  - Phase 1: Hindi, English
  - Phase 2: Bengali, Tamil, Telugu, Marathi, Gujarati
  - Phase 3: Kannada, Malayalam, Punjabi, Odia, Assamese
- Language selection at start of IVR call
- Consistent terminology across languages
- Cultural context and regional variations considered

### 4.6 User Management

- Automatic user profile creation on first interaction
- Profile stores: mobile number, language preference, location, demographic data
- Profile updates on subsequent interactions
- User can request profile deletion (privacy compliance)
- No personally identifiable information stored beyond necessary data
- Opt-out mechanism via SMS keyword "STOP"

## 5. Technical Requirements

### 5.1 AWS Services Architecture

| AWS Service | Purpose | Key Features |
|------------|---------|--------------|
| Amazon Bedrock | AI language understanding and scheme matching | Claude AI model for natural language processing, intent recognition, and eligibility analysis |
| Amazon Q | Development assistance and code generation | AI-powered development support for building and optimizing the platform |
| Amazon Connect | IVR system and call management | Cloud-based contact center, call routing, voice prompts, call recording |
| Amazon Lex | Conversational AI interface | Voice and text chatbot, intent recognition, slot filling, multi-turn conversations |
| Amazon Polly | Text-to-speech synthesis | Neural voices in Hindi and regional languages, natural-sounding speech output |
| Amazon Transcribe | Speech-to-text conversion | Real-time transcription, support for Indian accents and languages, custom vocabulary |
| AWS Lambda | Serverless backend processing | Event-driven functions for SMS processing, scheme matching, data retrieval, API integrations |
| Amazon DynamoDB | Scheme database and user profiles | NoSQL database for fast retrieval, scalable storage, low-latency queries |
| Amazon SNS | SMS gateway and notifications | SMS delivery, message queuing, delivery status tracking, multi-region support |
| Amazon S3 | Storage for audio files and logs | Voice recordings, call logs, scheme documents, backup storage |
| Amazon CloudWatch | Monitoring and logging | Performance metrics, error tracking, usage analytics, alerting |
| AWS IAM | Security and access control | Role-based access, encryption key management, API authentication |
| Amazon API Gateway | RESTful API management | API endpoints for integrations, rate limiting, request validation |
| Kiro | AI-assisted development platform | Code generation, testing, deployment automation, development acceleration |

### 5.2 Performance Requirements

- IVR callback initiation: < 5 seconds from SMS receipt
- Voice recognition accuracy: > 85% for Hindi and primary languages
- Concurrent call capacity: 10,000 simultaneous calls
- System uptime: 99.9% availability (< 9 hours downtime per year)
- Average call duration: 2-3 minutes
- SMS delivery time: < 30 seconds post-call
- Database query response time: < 100 milliseconds
- API response time: < 500 milliseconds for 95th percentile
- Voice latency: < 300 milliseconds for natural conversation flow

### 5.3 Scalability Requirements

- Year 1: Support 1 million users across 3 pilot states
- Year 2: Scale to 10 million users across 10 states
- Year 3: National rollout supporting 100 million users
- Language expansion: Start with 2 languages, scale to 10+ languages
- Scheme database: Start with 50 schemes, scale to 500+ schemes
- Geographic coverage: 3 states → 10 states → 28 states + 8 UTs
- Auto-scaling for peak usage (government announcement days, festival seasons)
- Horizontal scaling of Lambda functions and DynamoDB tables
- Multi-region deployment for disaster recovery and low latency

### 5.4 Data Storage Requirements

- Scheme database: 500+ schemes with eligibility criteria, documents, application process
- User profiles: Mobile number, language preference, location, demographic data (minimal PII)
- Call logs: Metadata only (duration, timestamp, outcome) - no audio storage beyond 30 days
- Analytics data: Aggregated usage statistics, scheme popularity, user demographics
- Backup and recovery: Daily backups, 30-day retention, point-in-time recovery

## 6. Non-Functional Requirements

### 6.1 Accessibility

- Zero internet requirement: Works on 2G/3G/4G networks via voice calls
- Zero smartphone requirement: Compatible with all feature phones
- Zero app installation: SMS and voice-based interaction only
- Voice-first design: No screen reading or typing required
- 24/7 availability: Service accessible at any time
- Toll-free or low-cost calling: Minimize user costs
- Simple interaction model: Maximum 5-6 questions per call
- Support for users with disabilities: Audio-only interface benefits visually impaired users

### 6.2 Localization

- Hindi as primary language with culturally appropriate terminology
- Support for 10+ Indian languages with regional variations
- Cultural context in voice prompts (greetings, tone, examples)
- Regional scheme awareness (state-specific programs)
- Festival and seasonal greetings
- Respectful addressing conventions (aap vs tum in Hindi)
- Local pronunciation of place names and scheme names

### 6.3 Cost Efficiency

- Target cost: < ₹5 per user interaction (SMS + IVR + processing)
- 100x cheaper than Common Service Center visits (₹500+)
- Optimized call duration to reduce telecom costs
- Efficient AI model usage to minimize Bedrock costs
- Serverless architecture to pay only for actual usage
- Bulk SMS pricing negotiations with telecom operators
- Free or subsidized service for end users (government-funded model)

### 6.4 Security & Privacy

- End-to-end encryption for data transmission
- No storage of sensitive personal information beyond necessary data
- Compliance with IT Act 2000 and data protection regulations
- User consent for call recording and data usage
- Secure API authentication for government database integrations
- Regular security audits and penetration testing
- Data anonymization for analytics and reporting
- User right to data deletion (GDPR-style compliance)
- Role-based access control for administrative functions
- Audit logs for all data access and modifications

### 6.5 Reliability

- 99.9% uptime SLA
- Automatic failover and disaster recovery
- Graceful degradation if AI services are temporarily unavailable
- Retry mechanisms for failed SMS or calls
- Error logging and alerting for rapid issue resolution
- Load balancing across multiple availability zones
- Regular backup and recovery testing

### 6.6 Usability

- Maximum 5-6 questions per IVR call
- Clear, simple voice prompts without jargon
- Option to repeat or skip questions
- Confirmation of understood information
- Friendly, conversational tone
- Minimal cognitive load for low-literacy users
- Consistent user experience across languages

## 7. Integration Requirements

### 7.1 Government Database Integrations

- National Scholarship Portal (NSP) for education schemes
- PM-KISAN portal for farmer benefits
- Ayushman Bharat for health schemes
- MGNREGA portal for employment schemes
- State government welfare portals (state-specific)
- Public Distribution System (PDS) database
- API-based integrations where available
- Web scraping or manual updates where APIs unavailable

### 7.2 Telecom Operator Integrations

- SMS gateway integration with major operators (Airtel, Jio, Vi, BSNL)
- Short code or long code provisioning for SMS triggers
- Bulk SMS pricing agreements
- Delivery status tracking and reporting
- Number validation and operator identification

### 7.3 Future Integration Roadmap

- DigiLocker integration for document verification
- Aadhaar authentication for identity verification (with user consent)
- UPI integration for application fee payments
- WhatsApp Business API for richer messaging (for smartphone users)
- Government e-marketplace (GeM) for scheme-related purchases
- Jan Dhan account verification for direct benefit transfer

### 7.4 Third-Party Services

- Payment gateway for premium features (future)
- Analytics platforms for usage insights
- CRM systems for user support and follow-up
- NGO and CSC partnerships for assisted applications

## 8. Success Metrics

### 8.1 User Metrics

- Pilot user acquisition: 10,000 users in first 3 months
- User retention: > 60% users make repeat inquiries
- Scheme uptake increase: 40% increase in scheme applications from users
- Average interaction time: < 2 minutes per call
- User satisfaction score: > 80% (via post-call survey)
- Call completion rate: > 90% of initiated calls completed
- Language diversity: Users across 5+ languages by end of Year 1

### 8.2 Business Impact Metrics

- Benefits unlocked: ₹50,000 crore in government benefits accessed by users
- Application time reduction: 50% reduction compared to CSC visits
- Cost reduction: 90% cost reduction compared to traditional access methods
- Geographic reach: Coverage across 100+ districts in pilot phase
- Scheme awareness: 3x increase in awareness of relevant schemes among users
- Application success rate: > 70% of users successfully apply for matched schemes

### 8.3 Technical Performance Metrics

- IVR callback time: < 5 seconds for 95% of requests
- Voice recognition accuracy: > 85% for Hindi, > 80% for regional languages
- System uptime: 99.9% availability
- SMS delivery success rate: > 98%
- Cost per interaction: < ₹5 per user
- Concurrent call capacity: 10,000 simultaneous calls without degradation
- API response time: < 500ms for 95th percentile
- Error rate: < 1% of total interactions

### 8.4 Social Impact Metrics

- Women users: > 40% of user base
- Senior citizen users: > 20% of user base
- First-time scheme applicants: > 60% of users
- Rural penetration: > 80% of users from rural areas
- Low-literacy users: > 50% of users with primary education or less

## 9. Timeline & Phases

### Phase 1: MVP Development (Months 1-2)

- Scope: Proof of concept with core functionality
- Features:
  - SMS trigger and IVR callback system
  - Hindi and English language support
  - Top 50 most popular central government schemes
  - Basic scheme matching algorithm
  - SMS results delivery
- Geographic coverage: 3 pilot states (Bihar, Uttar Pradesh, Madhya Pradesh)
- Target users: 10,000 pilot users
- AWS services: Core services (Connect, Lex, Polly, Transcribe, Lambda, DynamoDB, SNS)
- Success criteria: 80% call completion rate, 70% user satisfaction

### Phase 2: Scale & Enhancement (Months 3-6)

- Scope: Expanded coverage and improved AI
- Features:
  - 200+ government schemes (central + state)
  - 5 languages (Hindi, English, Bengali, Tamil, Telugu)
  - Enhanced AI matching with Amazon Bedrock
  - User profile management
  - Call quality improvements
  - Analytics dashboard
- Geographic coverage: 10 states across different regions
- Target users: 100,000 users
- Partnerships: NGOs, CSCs, government departments
- Success criteria: 85% call completion rate, 75% user satisfaction, 30% scheme uptake

### Phase 3: National Rollout (Months 7-12)

- Scope: Pan-India deployment
- Features:
  - 500+ government schemes (central + state + district)
  - 10+ Indian languages
  - Advanced AI with personalized recommendations
  - Integration with government databases (DigiLocker, Aadhaar)
  - Application tracking and follow-up
  - Multi-channel support (SMS, IVR, WhatsApp for smartphone users)
- Geographic coverage: All 28 states and 8 Union Territories
- Target users: 10 million users
- Partnerships: Government endorsement, telecom operator partnerships
- Success criteria: 90% call completion rate, 80% user satisfaction, 40% scheme uptake

## 10. Constraints & Assumptions

### 10.1 Technical Constraints

- Must work on 2G networks with limited bandwidth
- SMS character limit of 160 characters (or 70 for Unicode/Hindi)
- IVR call costs must be optimized (target < ₹2 per call)
- Voice recognition accuracy varies with accents and dialects
- Feature phone audio quality may be poor
- Network connectivity may be intermittent in rural areas
- Limited processing power on user devices (not applicable for cloud-based solution)

### 10.2 Business Constraints

- Government approval required for official endorsement
- Telecom operator partnerships needed for SMS short codes
- Funding required for initial development and operations
- User acquisition depends on awareness campaigns
- Scheme database maintenance requires ongoing effort
- Regulatory compliance with telecom and data protection laws

### 10.3 User Assumptions

- Users have access to a working mobile phone (feature phone or smartphone)
- Users can send SMS and receive calls
- Users have basic familiarity with phone calls
- Users are willing to share demographic information
- Users have some awareness of government schemes (even if limited)
- Users can understand spoken Hindi or regional language

### 10.4 Technical Assumptions

- AWS services are available and reliable in India region
- Amazon Transcribe supports Indian accents with acceptable accuracy
- Amazon Polly provides natural-sounding Hindi voices
- Telecom operators provide reliable SMS and voice services
- Government scheme data is accessible (via APIs or manual collection)
- Internet connectivity is available for backend services (not for end users)

## 11. Risk Mitigation

### 11.1 Technical Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|---------------------|
| Voice recognition accuracy below 85% for diverse accents | High | Medium | Fine-tune Amazon Transcribe with Indian accent datasets; implement fallback to DTMF input; continuous model improvement |
| High IVR call costs exceed budget | High | Medium | Optimize call duration; negotiate bulk rates with telecom operators; implement call-back queuing during peak times |
| AWS service outages | High | Low | Multi-region deployment; automatic failover; graceful degradation to basic functionality |
| SMS delivery failures | Medium | Medium | Multiple SMS gateway providers; retry mechanism; alternative delivery via voice message |
| Database scalability issues | Medium | Low | DynamoDB auto-scaling; caching layer; query optimization |
| Integration failures with government databases | Medium | High | Fallback to manual scheme database; periodic data synchronization; error handling and logging |

### 11.2 Business Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|---------------------|
| Low user adoption | High | Medium | Partner with NGOs and SHGs for awareness; government endorsement; word-of-mouth campaigns; free service |
| Lack of government support | High | Low | Demonstrate value through pilot; engage with government stakeholders early; align with Digital India mission |
| Funding constraints | High | Medium | Phased approach with MVP first; seek government grants; CSR funding; impact investor interest |
| Competition from existing solutions | Medium | Low | Differentiate with voice-first, zero-internet approach; focus on underserved rural segment |
| Scheme database maintenance burden | Medium | High | Automate data collection where possible; partner with government departments; crowdsource updates |

### 11.3 Operational Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|---------------------|
| Customer support overload | Medium | Medium | Self-service IVR for common queries; FAQ SMS responses; tiered support model |
| Data privacy breaches | High | Low | Strong encryption; minimal data collection; regular security audits; compliance with regulations |
| Misuse or spam | Medium | Medium | Rate limiting; user verification; abuse detection algorithms; block list management |
| Language translation errors | Medium | Medium | Native speaker review; user feedback mechanism; continuous improvement |

## 12. Future Enhancements

### 12.1 Application Tracking (Phase 4)

- Track application status after submission
- SMS notifications for application updates
- Integration with government portals for real-time status
- Reminder system for pending documents or actions

### 12.2 Document Assistance (Phase 4)

- OCR for document scanning via smartphone camera (for smartphone users)
- Document checklist and verification
- Integration with DigiLocker for digital document access
- Guidance on obtaining missing documents

### 12.3 Multi-Scheme Application (Phase 5)

- Apply for multiple schemes in single interaction
- Bulk document upload and reuse
- Family-level scheme recommendations
- Household benefit optimization

### 12.4 Community Support (Phase 5)

- Connect users with local volunteers or CSC operators
- Peer support groups for scheme applicants
- Success stories and testimonials
- Community awareness campaigns

### 12.5 Grievance Redressal (Phase 5)

- Report issues with scheme applications
- Track grievance status
- Escalation to appropriate authorities
- Feedback loop for system improvement

### 12.6 Advanced AI Features (Phase 6)

- Predictive scheme recommendations based on life events
- Personalized follow-up based on user journey
- Sentiment analysis for user satisfaction
- Multilingual chatbot for text-based queries (WhatsApp, web)

### 12.7 Financial Inclusion (Phase 6)

- Integration with Jan Dhan accounts
- Direct benefit transfer tracking
- Microfinance and loan scheme information
- Financial literacy content

### 12.8 Expanded Services (Phase 7)

- Job matching and employment schemes
- Skill development program recommendations
- Healthcare scheme enrollment and appointment booking
- Agricultural advisory services (weather, crop prices, best practices)

---

## Document Control

- Version: 1.0
- Last Updated: February 14, 2026
- Owner: Bharat Sahayak Development Team
- Status: Draft for Hackathon Submission
- Next Review: Post-hackathon feedback incorporation
