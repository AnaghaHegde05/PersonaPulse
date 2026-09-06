# PersonaPulse AI

### AI-Powered Multi-Platform Content Personalization

PersonaPulse AI is a serverless content personalization platform that transforms a single content idea into platform-specific, audience-aware content using **Amazon Bedrock**.

The application allows users to provide an idea, select a target platform, audience, and tone, and receive structured content containing a hook, main content, call-to-action, hashtags, and an engagement score.

Built as part of the **AI for Bharat Hackathon**, the project demonstrates how generative AI can be integrated into a practical content creation workflow using AWS serverless services.

---

## Features

* Generate content from a single idea
* Customize content for different platforms
* Select a target audience
* Customize the tone of generated content
* Generate structured content with:

  * Hook
  * Content
  * Call-to-action
  * Hashtags
* Rule-based engagement scoring
* AI-powered prompt conditioning
* Serverless backend using AWS Lambda and Amazon Bedrock
* React-based web interface

### Supported Platforms

* LinkedIn
* Instagram
* Twitter/X
* YouTube
* Blog

---

## How It Works

```text
User
  │
  ▼
React Frontend
  │
  │ POST /generate
  ▼
Amazon API Gateway
  │
  ▼
AWS Lambda
  │
  ├── Input Validation
  ├── Prompt Construction
  ├── Engagement Scoring
  │
  ▼
Amazon Bedrock
  │
  ▼
Structured Content
  │
  ▼
React Frontend
```

The frontend collects the user's content idea and preferences and sends them to the backend through an API Gateway endpoint.

The Lambda function builds a platform- and audience-aware prompt and sends it to **Amazon Bedrock (Amazon Nova Micro)**. The generated response is parsed into a structured format and returned to the frontend along with an engagement score.

---

## Tech Stack

### Frontend

* React
* JavaScript
* HTML
* CSS

### Backend

* Python
* AWS Lambda
* Amazon API Gateway
* Amazon Bedrock
* Boto3

### AI

* Amazon Nova Micro
* Prompt Engineering
* Structured JSON Generation

### Cloud & Infrastructure

* AWS IAM
* AWS CloudWatch
* Serverless Architecture

---

## Architecture

PersonaPulse follows a lightweight serverless architecture:

```text
┌────────────────────┐
│    React Frontend  │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│   API Gateway      │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│    AWS Lambda      │
│                    │
│ • Validation       │
│ • Prompt Building  │
│ • AI Orchestration │
│ • Scoring          │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│  Amazon Bedrock    │
│   Nova Micro       │
└────────────────────┘
```

The current implementation is **stateless** and does not require a persistent database.

---

## API

### `POST /generate`

Generates personalized content based on the provided input.

#### Request

```json
{
  "idea": "AI transforming rural education",
  "platform": "LinkedIn",
  "audience": "Students",
  "tone": "Professional"
}
```

#### Response

```json
{
  "hook": "...",
  "content": "...",
  "cta": "...",
  "hashtags": "...",
  "engagement_score": 85
}
```

---

## Engagement Scoring

PersonaPulse includes a lightweight engagement scoring mechanism to provide a quick estimate of content engagement potential.

The current scoring logic considers factors such as:

* Presence of questions
* Use of exclamation marks
* Content length
* Presence of a call-to-action

The score is normalized to a maximum of **100**.

> The engagement score is a heuristic score and is not a machine-learning prediction model.

---

## Project Structure

```text
PersonaPulse/
│
├── backend/
│   ├── bedrock_client.py
│   ├── engagement_scoring.py
│   ├── lambda_handler.py
│   ├── prompt_engine.py
│   └── requirements.txt
│
├── frontend/
│   ├── public/
│   └── src/
│
├── docs/
│   ├── technical_blog_draft.md
│   └── video_pitch_script.md
│
├── infrastructure/
│   ├── architecture_diagram.png
│   └── aws_setup.md
│
├── design.md
├── requirements.md
├── README.md
└── LICENSE
```

---

## Running Locally

### 1. Clone the repository

```bash
git clone <repository-url>
cd PersonaPulse
```

### 2. Install frontend dependencies

```bash
cd frontend
npm install
```

### 3. Start the frontend

```bash
npm start
```

The React application will run at:

```text
http://localhost:3000
```

### Backend

The backend is designed to run through **AWS Lambda** and requires access to Amazon Bedrock.

AWS configuration and deployment details are available in:

```text
infrastructure/aws_setup.md
```

---

## AWS Services

| Service            | Purpose                          |
| ------------------ | -------------------------------- |
| Amazon Bedrock     | Generative AI content generation |
| AWS Lambda         | Serverless backend processing    |
| Amazon API Gateway | REST API endpoint                |
| AWS IAM            | Access control and permissions   |
| Amazon CloudWatch  | Logging and monitoring           |

---

## Why Generative AI?

Traditional rule-based systems can modify predefined templates, but they struggle with understanding context and adapting content naturally across different platforms and audiences.

PersonaPulse uses generative AI for:

* Context-aware content generation
* Platform-specific adaptation
* Audience personalization
* Tone transformation
* Structured content generation

Prompt conditioning is used to guide the model toward consistent, structured responses.

---

## Future Improvements

Potential extensions include:

* Brand voice customization
* Multi-platform batch generation
* Content versioning
* A/B content generation
* Content calendar integration
* Analytics dashboard
* User authentication
* Persistent content storage
* Automated deployment infrastructure

These features are **not part of the current implementation** and represent possible future development.

---

## Hackathon

Built for the **AI for Bharat Hackathon**.

### Focus

**Meaningful AI for real-world content and digital experiences**

The project explores how generative AI and serverless cloud infrastructure can reduce the effort required to adapt content for different audiences and platforms.

---

## License

This project is licensed under the **MIT License**.
