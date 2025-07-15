# 🗺️ MindRoute - AI-Powered Learning Roadmap Generator

[![Next.js](https://img.shields.io/badge/Next.js-15.1.8-black)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-19.1.0-blue)](https://reactjs.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4.1-38B2AC)](https://tailwindcss.com/)
[![Supabase](https://img.shields.io/badge/Supabase-2.49.8-green)](https://supabase.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> Transform your learning goals into interactive, personalized roadmaps with AI-powered insights and community-driven content.

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/nk2552003/tattva.git

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local

# Run development server
npm run dev
```

Visit `http://localhost:3000/pages/mindroute` to start creating your learning roadmap!

## 📖 Table of Contents

### 🏗️ **Getting Started**
1. [Overview](#overview)
2. [Features](#features)
3. [Installation](#installation)
4. [Environment Setup](#environment-setup)

### 🛠️ **Development Guide**
5. [Architecture & Technology Stack](#architecture--technology-stack)
6. [Project Structure](#project-structure)
7. [User Flow & Functionality](#user-flow--functionality)
8. [UI Components Guide](#ui-components-guide)

### 📚 **Technical Documentation**
9. [API Reference](#api-reference)
10. [Database Schema](#database-schema)
11. [Tree-to-Flow Algorithm](#tree-to-flow-algorithm)
12. [Background Jobs](#background-jobs)

### 🎨 **Design & Assets**
13. [UI Design System](#ui-design-system)
14. [Component Library](#component-library)
15. [Responsive Design](#responsive-design)

### 🚀 **Deployment & Production**
16. [Deployment Guide](#deployment-guide)
17. [Environment Variables](#environment-variables)
18. [Performance Optimization](#performance-optimization)

### 🔧 **Extending & Customizing**
19. [Customization Guide](#customization-guide)
20. [Contributing](#contributing)
21. [Troubleshooting](#troubleshooting)

---

## 🌟 Overview

**MindRoute** is an intelligent learning roadmap generator that transforms your educational goals into interactive, personalized learning paths. Built with modern web technologies and powered by AI, it provides:

### 🎯 **Core Features**
- **AI-Powered Generation**: Create custom learning roadmaps using GPT-4
- **Interactive Visualization**: Navigate through your learning journey with React Flow
- **Community Sharing**: Discover and share roadmaps with the community
- **Progress Tracking**: Monitor your learning progress with visual indicators
- **Multi-Format Content**: Courses, projects, and FAQ sections for comprehensive learning
- **Responsive Design**: Seamless experience across desktop, tablet, and mobile

### 🔧 **Key Capabilities**
- Generate roadmaps for any learning topic
- Personalize based on skill level and learning style
- Export roadmaps in multiple formats
- Real-time collaboration and sharing
- Integration with external learning resources

## ✨ Features

### 🤖 **AI-Powered Roadmap Generation**
- **Smart Input Form**: Collect learning goals, duration, skill level, and preferences
- **GPT-4 Integration**: Generate structured, comprehensive learning paths
- **Background Processing**: Inngest-powered job queue for seamless user experience
- **Customizable Prompts**: Tailor AI responses to specific learning domains

### 🎨 **Interactive Visualization**
- **Dynamic Flowcharts**: Navigate learning paths with React Flow
- **Custom Node System**: Color-coded topics with hierarchical organization
- **Multiple View Modes**: Switch between flowchart and tree hierarchy
- **Zoom & Pan Controls**: Explore large roadmaps with ease

### 📚 **Comprehensive Content**
- **Roadmap Tab**: Interactive flowchart with clickable nodes
- **Courses Tab**: Curated course recommendations
- **Projects Tab**: Hands-on projects and templates
- **FAQ Tab**: Common questions and expert answers

### 👥 **Community Features**
- **Public Roadmaps**: Browse featured community roadmaps
- **Private Workspaces**: Create and manage personal roadmaps
- **Sharing System**: Generate shareable links for collaboration
- **User Authentication**: Secure access with Clerk integration

## 🛠️ Installation

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Supabase account
- Clerk account (for authentication)
- OpenAI API key (for AI generation)

### Step-by-Step Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/tattva.git
   cd tattva
   ```

2. **Install Dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Environment Configuration**
   ```bash
   cp .env.example .env.local
   ```

4. **Configure Environment Variables**
   ```env
   # Supabase Configuration
   NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_key

   # Clerk Authentication
   NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
   CLERK_SECRET_KEY=your_clerk_secret_key

   # AI Integration
   GITHUB_TOKEN=your_github_token_for_models_api
   OPENAI_API_KEY=your_openai_api_key

   # Inngest Configuration
   INNGEST_EVENT_KEY=your_inngest_event_key
   INNGEST_SIGNING_KEY=your_inngest_signing_key
   ```

5. **Database Setup**
   ```bash
   # Run Supabase migrations
   npx supabase db push

   # Seed initial data (optional)
   npx supabase db seed
   ```

6. **Start Development Server**
   ```bash
   npm run dev
   ```

   Visit `http://localhost:3000/pages/mindroute` to see MindRoute in action!

## 🏗️ Architecture & Technology Stack  

MindRoute is built on a modern, scalable architecture that combines the best of React ecosystem with powerful AI capabilities:

### 🔧 **Core Technologies**

#### **Frontend Framework**
- **Next.js 15.1.8**: App Router, Server Components, API Routes
- **React 19.1.0**: Functional components with modern hooks
- **TypeScript 5.x**: Full type safety and developer experience

#### **Styling & UI**
- **Tailwind CSS 3.4.1**: Utility-first styling with custom design system
- **React Flow 11.11.4**: Interactive flowchart visualization
- **Framer Motion 12.15.0**: Smooth animations and transitions
- **Lucide React**: Modern icon library

#### **Data & State Management**
- **Supabase 2.49.8**: PostgreSQL database with real-time subscriptions
- **Clerk 6.20.0**: Authentication and user management
- **React Context**: Global state management
- **Inngest 3.38.0**: Background job processing

#### **AI & External APIs**
- **OpenAI GPT-4**: Via GitHub Models API for roadmap generation
- **Custom Prompts**: Engineered for educational content generation
- **Background Processing**: Async AI generation with progress tracking

### 📁 **Project Structure**

```
tattva/
├── 📱 app/                           # Next.js App Router
│   ├── 🏠 pages/mindroute/          # Main MindRoute interface
│   │   ├── page.tsx                 # Landing page with form
│   │   └── _components/             # Page-specific components
│   │       ├── form_comp.tsx        # Input form
│   │       ├── header_2.tsx         # Page header
│   │       └── RoadmapGrip.tsx      # Roadmap grid display
│   │
│   ├── 🗺️ (routes)/roadmap/[libid]/ # Dynamic roadmap pages
│   │   ├── page.tsx                 # Roadmap visualization
│   │   └── _components/             # Roadmap components
│   │       ├── CustomNode.tsx       # Interactive nodes
│   │       ├── HierarchyModal.tsx   # Tree view
│   │       ├── LoadingStatus.tsx    # Progress indicators
│   │       └── tabs/                # Content tabs
│   │           ├── roadmap-tab.tsx  # Flowchart view
│   │           ├── courses-tab.tsx  # Course recommendations
│   │           ├── projects-tab.tsx # Project suggestions
│   │           └── faq_questions-tab.tsx # FAQ section
│   │
│   ├── 🔌 api/                      # Backend API routes
│   │   ├── roadmap/route.ts         # Roadmap generation
│   │   ├── roadmap-extra-data/      # Additional content
│   │   └── generate-hierarchy-json/ # Tree structure API
│   │
│   ├── 🧩 components/               # Shared components
│   │   ├── types/roadmap.ts         # TypeScript interfaces
│   │   └── utils/                   # Utility functions
│   │       ├── tree-to-flow.ts      # Converts tree to flowchart
│   │       ├── helpers.ts           # Common utilities
│   │       └── prompt.ts            # AI prompt templates
│   │
│   └── 🔧 services/                 # External integrations
│       ├── supabase.tsx             # Database client
│       └── constants.ts             # Configuration
│
├── ⚡ inngest/                      # Background jobs
│   ├── client.ts                    # Inngest configuration
│   └── functions.ts                 # Job definitions
│
├── 🎨 public/                       # Static assets
└── 📝 docs/                         # Documentation
    ├── mindroute-user-flow.md       # User flow diagrams
    └── mindroute-ui-design-guide.md # UI component guide
```

## 🌊 User Flow & Functionality

For detailed user flow documentation, see: **[MindRoute User Flow Guide](./mindroute-user-flow.md)**

### 🎯 **Core User Journey**

```mermaid
graph TD
    A[User visits MindRoute] --> B[Fill learning form]
    B --> C[AI generates roadmap]
    C --> D[Interactive visualization]
    D --> E[Explore content tabs]
    E --> F[Share & collaborate]
```

### 📝 **Step-by-Step Process**

1. **Input Collection**
   - Learning goal (e.g., "Frontend Developer")
   - Duration preference (e.g., "12 weeks")
   - Weekly time commitment
   - Current skill level
   - Learning style preference

2. **AI Processing**
   - Background job triggered via Inngest
   - GPT-4 generates structured roadmap
   - Content saved to Supabase database

3. **Visualization**
   - Tree-to-flow algorithm converts data
   - Interactive React Flow component renders
   - Color-coded hierarchical layout

4. **Content Exploration**
   - Navigate flowchart nodes
   - Switch between content tabs
   - Access courses, projects, and FAQ

5. **Collaboration**
   - Share roadmap with unique URLs
   - Public/private visibility options
   - Community discovery features

## 🎨 UI Components Guide

For comprehensive UI documentation, see: **[MindRoute UI Design Guide](./mindroute-ui-design-guide.md)**

### 🧩 **Core Components**

#### **Form Component** (`form_comp.tsx`)
- Multi-field input collection
- Real-time validation
- Dropdown menus with icons
- Progress indication

#### **Interactive Flowchart** (`CustomNode.tsx`)
- Custom React Flow nodes
- Color-coded hierarchy
- Hover and click interactions
- Connection handles

#### **Tab Navigation** (`tab-navigation.tsx`)
- Four content sections
- Smooth transitions
- Mobile-responsive
- Progress indicators

#### **Loading States** (`LoadingStatus.tsx`)
- Progressive loading bars
- Status message updates
- Skeleton animations
- Error handling

### 🎨 **Design System**

#### **Color Palette**
- **Primary**: `#178d73` (Teal green)
- **Background**: `#131a19` (Dark gray-green)
- **Borders**: `#2d3d3b` (Medium gray-green)
- **Text**: White with gray placeholders

#### **Typography**
- **Headers**: 2.5rem, bold, tight letter-spacing
- **Body**: 1rem, regular, 1.6 line-height
- **Captions**: 0.875rem, medium, 0.8 opacity

## 📚 API Reference

### 🔌 **Core Endpoints**

#### **POST** `/api/roadmap`
Generate a new roadmap with AI assistance.

**Request Body:**
```json
{
  "libId": "uuid-string",
  "formData": {
    "goal": "Frontend Developer",
    "duration": "12 Weeks",
    "weeklyHours": "10 Hours/week",
    "skillLevel": "beginner",
    "learningStyle": "mixed"
  }
}
```

**Response:**
```json
{
  "inngestRunId": "job-id-string",
  "status": "processing"
}
```

#### **GET** `/api/roadmap-extra-data`
Fetch additional content for existing roadmaps.

#### **POST** `/api/generate-hierarchy-json`
Convert AI response to structured hierarchy.

### 🗄️ **Database Schema**

#### **Library Table**
```sql
CREATE TABLE Library (
  id SERIAL PRIMARY KEY,
  libId UUID UNIQUE NOT NULL,
  userEmail TEXT,
  searchInput TEXT,
  type TEXT DEFAULT 'roadmap',
  created_at TIMESTAMP DEFAULT NOW()
);
```

#### **Roadmap Table**
```sql
CREATE TABLE Roadmap (
  id SERIAL PRIMARY KEY,
  libId UUID REFERENCES Library(libId),
  FormData JSONB,
  AiResp JSONB,
  Visiblity TEXT DEFAULT 'private',
  created_at TIMESTAMP DEFAULT NOW()
);
```

## 🧠 Tree-to-Flow Algorithm

The core visualization algorithm converts hierarchical AI responses into interactive flowcharts:

### 🌳 **Algorithm Overview**

```typescript
export function generateSpineFlow(topic: string, tree: TopicNode[]) {
  // 1. Create central spine with main topics
  // 2. Branch child topics horizontally (alternating sides)
  // 3. Calculate optimal positioning
  // 4. Generate React Flow nodes and edges
  
  return { nodes, edges };
}
```

### 📐 **Layout Strategy**
- **Central Spine**: Vertical sequence of main topics
- **Horizontal Branches**: Child topics extend left/right
- **Dynamic Spacing**: Adjusts based on content hierarchy
- **Connection Handles**: Proper edge routing between nodes

For complete implementation details, see: **[Tree-to-Flow Documentation](./mindroute-user-flow.md#tree-to-flow-conversion-implementation)**

## ⚡ Background Jobs

MindRoute uses Inngest for reliable background processing:

### 🔄 **Job Types**

#### **RoadmapModel Job**
- Processes form data with AI
- Generates structured learning path
- Saves results to database
- Handles errors and retries

#### **RoadmapExtraData Job**
- Fetches course recommendations
- Generates project suggestions
- Populates FAQ content
- Updates existing roadmaps

### 📊 **Job Monitoring**
- Real-time status updates
- Progress indicators in UI
- Error logging and alerts
- Performance metrics

## 🚀 Deployment Guide

### 🌐 **Vercel Deployment**

1. **Connect Repository**
   ```bash
   # Install Vercel CLI
   npm i -g vercel
   
   # Deploy to Vercel
   vercel --prod
   ```

2. **Environment Variables**
   Configure all required environment variables in Vercel dashboard

3. **Domain Configuration**
   Set up custom domain and SSL certificates

### 🔧 **Environment Variables**

```env
# Database
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key

# Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...

# AI Services
GITHUB_TOKEN=github_pat_...
OPENAI_API_KEY=sk-...

# Background Jobs
INNGEST_EVENT_KEY=...
INNGEST_SIGNING_KEY=...
```