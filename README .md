# 🇮🇳 Bharat Sahayak - AI for Every Indian

> **Voice-first AI solution to bridge the gap between government schemes and rural India**

[![AWS Powered](https://img.shields.io/badge/AWS-Powered-orange)](https://aws.amazon.com)
[![Amazon Bedrock](https://img.shields.io/badge/Amazon-Bedrock-blue)](https://aws.amazon.com/bedrock)
[![Hackathon](https://img.shields.io/badge/AWS-AI%20for%20Bharat%202026-green)](https://hack2skill.com)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🎯 Problem Statement

**65% of government schemes never reach their intended beneficiaries**, resulting in **₹1.47 lakh crore in unclaimed welfare funds** annually in India.

### Why?

- 📱 **500M+ Indians use feature phones** - no smartphone, no internet
- 🌐 **Only 31% rural internet penetration** vs 67% urban
- 📖 **300M+ citizens have limited literacy** - can't navigate complex portals
- 🏢 **Existing solutions assume** digital access and literacy

**The Gap:** Half a billion feature phone users are unreachable by Digital India initiatives.

---

## 💡 Our Solution

**Bharat Sahayak** is a voice-first, SMS-based AI assistant that works on **ANY phone** - no smartphone or internet needed.

### How It Works

```
1. 📲 User sends SMS "SCHEME" to short code
2. 📞 IVR calls back within 5 seconds
3. 🗣️ Voice conversation in Hindi/regional languages
4. 🤖 AI matches user profile to 500+ schemes
5. 📨 SMS delivered with personalized results

⏱️ Total Time: 2 minutes
💰 Total Cost: ₹5 vs ₹500 at CSC
```

---

## ✨ Key Features

### 🌟 Zero Barriers
- ✅ No internet required
- ✅ No smartphone needed
- ✅ No app installation
- ✅ No reading/writing needed
- ✅ Works 24/7

### 🗣️ Voice-First Design
- Natural Hindi conversation
- Support for 10+ regional languages
- Optimized for Indian accents
- Interactive eligibility questions

### 🎯 AI-Powered Matching
- 500+ government schemes database
- Complex eligibility rule matching
- Personalized recommendations
- Real-time processing

### 💰 Cost-Effective
- **₹5 per user** vs ₹500 CSC visit
- 100x cheaper than traditional methods
- Serverless = pay only for usage
- Optimized for low-bandwidth

---

## 🏗️ Architecture

### System Overview

```
┌─────────────┐         ┌──────────────┐         ┌─────────────┐
│   User      │  SMS    │  Amazon SNS  │ Trigger │ AWS Lambda  │
│ Feature     │────────▶│  (Gateway)   │────────▶│(Orchestrator)│
│   Phone     │         └──────────────┘         └──────┬──────┘
└─────┬───────┘                                          │
      │                                                  │ Initiate Call
      │ ◀──────────────────────────────────────────────┘
      │
      │ Voice Conversation
      ▼
┌──────────────────────────────────────────────────────────────┐
│              Communication Layer (Amazon Connect)             │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────────┐     │
│  │ Amazon Lex  │  │Amazon Polly │  │Amazon Transcribe │     │
│  │   (NLU)     │  │   (TTS)     │  │     (STT)        │     │
│  └─────────────┘  └─────────────┘  └──────────────────┘     │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│                    AI Processing Layer                        │
│  ┌──────────────────┐         ┌──────────────────┐           │
│  │ Amazon Bedrock   │         │   Amazon Q       │           │
│  │ (Claude Sonnet)  │         │  (Dev Assistant) │           │
│  │ Scheme Matching  │         │                  │           │
│  └──────────────────┘         └──────────────────┘           │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│                      Data Layer                               │
│  ┌──────────────────────────────────────────────────┐        │
│  │        Amazon DynamoDB                            │        │
│  │  - Schemes Database (500+ schemes)                │        │
│  │  - User Profiles & Sessions                       │        │
│  └──────────────────────────────────────────────────┘        │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌─────────────┐         ┌──────────────┐
│   User      │  SMS    │  Amazon SNS  │
│  Receives   │◀────────│  (Results)   │
│  Results    │         └──────────────┘
└─────────────┘
```

> 📊 **View detailed architecture diagram:** [bharat-sahayak-architecture.svg](./bharat-sahayak-architecture.svg)

### Built With AWS AI Services

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **AI/ML** | Amazon Bedrock (Claude) | Language understanding, scheme matching |
| **Voice** | Amazon Connect, Lex, Polly, Transcribe | IVR, NLU, TTS, STT |
| **Compute** | AWS Lambda | Serverless business logic |
| **Database** | Amazon DynamoDB | Scheme data, user sessions |
| **Messaging** | Amazon SNS | SMS gateway |
| **Development** | Kiro, Amazon Q | AI-assisted coding, architecture guidance |
| **Monitoring** | CloudWatch, X-Ray | Metrics, logs, tracing |

---

## 📊 Impact Potential

### Target Reach
- **500M+** feature phone users in rural India
- **300M+** low-literacy citizens
- **28 states + 8 UTs** coverage
- **10+** regional languages

### Expected Outcomes
- 📈 **40% increase** in scheme uptake
- 💵 **₹50,000 crore** unlocked benefits annually
- ⏱️ **50% reduction** in application time
- 💰 **90% cost reduction** vs traditional methods

---

## 🚀 Getting Started

### Prerequisites

- AWS Account with credits (AWS Educate recommended for students)
- GitHub Student Developer Pack (includes Twilio credits)
- Basic understanding of Python and AWS services

### Quick Start

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/bharat-sahayak.git

# Navigate to project
cd bharat-sahayak

# Read the documentation
cat requirements.md
cat design.md
```

### AWS Setup

1. **Enable AWS Services:**
   - Amazon Bedrock (Claude 3 Sonnet)
   - Amazon Connect (IVR)
   - Amazon Lex (NLU)
   - Amazon SNS (SMS)
   - AWS Lambda (Compute)
   - Amazon DynamoDB (Database)

2. **Configure Environment:**
   - Set up Amazon Connect instance
   - Create Lex bot with Hindi language support
   - Configure SNS for SMS gateway
   - Deploy Lambda functions

3. **Deploy:**
   - Use AWS SAM or CloudFormation templates
   - Configure environment variables
   - Test with sample phone number

---

## 📁 Repository Structure

```
bharat-sahayak/
├── README.md                        # This file
├── requirements.md                  # Detailed project requirements
├── design.md                       # Technical design document
├── bharat-sahayak-architecture.svg # System architecture diagram
├── LICENSE                         # MIT License
└── .gitignore                      # Python gitignore
```

---

## 🎥 Demo

### User Journey Example

```
Ramesh (Farmer, 45, Bihar, Feature Phone)
    ↓
Sends SMS: "SCHEME" to 56677
    ↓
Receives IVR call in 5 seconds
    ↓
IVR (Hindi): "Namaste! Aap kis yojana ke liye jaanna chahte hain?"
    ↓
Ramesh: "Mujhe kisan yojana chahiye"
    ↓
IVR: "Aapki umar kya hai?" → "45"
IVR: "Aapke paas kitni zameen hai?" → "2 acre"
    ↓
AI Processing: age=45, occupation=farmer, land=2 acres
    ↓
Match Found: PM-KISAN (100% eligible)
    ↓
SMS Received: "You are eligible for PM-KISAN. ₹6000/year. Apply: pmkisan.gov.in"
    ↓
✅ Total Time: 2 minutes
```

---

## 🏆 Why Bharat Sahayak Wins

### Unique Advantages

| Feature | Bharat Sahayak | MyScheme.gov.in | CSC Centers |
|---------|----------------|-----------------|-------------|
| Works on feature phones | ✅ | ❌ | ❌ |
| No internet needed | ✅ | ❌ | ❌ |
| No literacy needed | ✅ | ❌ | ❌ |
| 24/7 availability | ✅ | ✅ | ❌ |
| Cost per user | ₹5 | Free* | ₹500 |
| Reach | 500M | 100M | Limited |

*Requires smartphone + internet + digital literacy

---

## 🗺️ Roadmap

### Phase 1: MVP (Months 1-2)
- Top 50 central schemes
- Hindi + English
- 3 states (Bihar, UP, Rajasthan)
- 10,000 users

### Phase 2: Scale (Months 3-6)
- 200+ schemes (state-level)
- 5 additional languages
- 10 states
- 100,000 users

### Phase 3: National (Months 6-12)
- All 500+ schemes
- 10+ languages
- Pan-India deployment
- 10M+ users

---

## 👥 Team

**Team Bharat Sahayak**

- **[Your Name]** - [Role] - [LinkedIn/GitHub]
- **[Member 2]** - [Role] - [LinkedIn/GitHub]
- **[Member 3]** - [Role] - [LinkedIn/GitHub]
- **[Member 4]** - [Role] - [LinkedIn/GitHub]

**Hackathon:** AWS AI for Bharat 2026

---

## 📞 Contact

- **Email:** [your-email@college.edu]
- **Hackathon Platform:** [Your H2S profile link]
- **Project Link:** [https://github.com/YOUR_USERNAME/bharat-sahayak](https://github.com/YOUR_USERNAME/bharat-sahayak)

---

## 📄 Documentation

- 📋 [Requirements Document](./requirements.md) - Detailed project requirements
- 🏗️ [Design Document](./design.md) - Technical architecture and implementation
- 📊 [Architecture Diagram](./bharat-sahayak-architecture.svg) - Visual system overview

---

## 🙏 Acknowledgments

**Built with:**
- Amazon Web Services (AWS)
- Amazon Bedrock & Claude AI
- Kiro IDE
- Amazon Q

**Special Thanks:**
- AWS AI for Bharat Hackathon organizers
- Anthropic (Claude AI)
- Our mentors and supporters
- The 500M+ rural Indians who inspire this work

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🌟 Support

If you believe in digital inclusion for all, please **⭐ star this repository**!

---

<div align="center">

### "Because true Digital India means reaching those WITHOUT smartphones"

**Made with ❤️ for rural India | Powered by AWS**

🇮🇳 **Bharat Sahayak - AI for Every Indian** 🇮🇳

</div>
