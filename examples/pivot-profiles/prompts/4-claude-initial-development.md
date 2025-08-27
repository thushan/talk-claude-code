# Pivot Profiles MVP - Multi-Agent Development Orchestration

## Project Overview
Build **Pivot Profiles** - a system that transforms static consultant YAML profiles (like Thushan's in profiles/thushan.yaml) into trackable, shareable digital experiences with engagement analytics.

## Multi-Agent Architecture

```
[Product Owner - Claude Opus] (You - Orchestrator)
    ├── [Tech Lead - Claude Opus] → System architecture & API contracts
    │   ├── [Backend Developer - Claude Sonnet] → API, database, analytics
    │   ├── [Frontend Developer - Claude Sonnet] → React components & UX
    │   └── [DevOps Engineer - Claude Sonnet] → Docker, deployment, CI/CD
    ├── [Business Analyst - Claude Sonnet] → Requirements validation & acceptance testing
    └── [QA Lead - Claude Sonnet] → Technical testing, edge cases, automation
```

Ensure you use:
- serena for semantic code retrieval and editing tools
- context7 for up to date documentation on third party code
- sequential thinking for any decision making

Create a concise claude.md file at the end.

Ask any clarifying questions or confirm your understanding before you start.

## GIT WORKFLOW & COLLABORATION PROTOCOL

### 🌳 Git Branch Strategy

**Repository Structure:**
```
pivot-profiles/
├── main (production-ready code)
├── develop (integration branch)
├── feature/tech-lead-architecture
├── feature/backend-api-endpoints  
├── feature/frontend-sales-composer
├── feature/frontend-client-viewer
├── feature/devops-docker-setup
├── feature/qa-test-automation
└── feature/ba-acceptance-criteria
```

### 📋 Agent Git Responsibilities

**All Development Agents Must:**

1. **Create Feature Branches**
   ```bash
   # Example for Backend Developer
   git checkout develop
   git pull origin develop
   git checkout -b feature/backend-share-management
   ```

2. **Regular Commits with Structured Messages**
   ```bash
   git commit -m "feat(api): implement share creation endpoint
   
   - Add POST /api/shares with validation
   - Include JWT token generation
   - Add consultant selection logic
   - Include expiry date handling
   
   Refs: #USER_STORY_123"
   ```

3. **Commit Frequency Requirements**
   - **Minimum**: Every major feature completion
   - **Recommended**: Every logical code change (multiple times per session)
   - **Critical**: Before switching contexts or stopping work

4. **Pull Request Protocol**
   ```markdown
   ## PR Title: [Component] Brief description
   
   ### Changes Made
   - List specific implementations
   - Reference user stories/requirements
   
   ### Testing Performed
   - Unit tests added/updated
   - Manual testing scenarios
   
   ### Business Analyst Review Required
   - [ ] Feature matches acceptance criteria
   - [ ] Business logic implemented correctly
   - [ ] User workflow functions as specified
   
   ### QA Review Required  
   - [ ] Technical implementation sound
   - [ ] Edge cases handled
   - [ ] Integration points working
   ```

### 🔍 Business Analyst Git Integration

**Your Git Workflow:**
1. **Monitor Feature Branches**
   - Review commits for business logic alignment
   - Test feature branches against requirements
   - Comment on PRs with acceptance feedback

2. **Requirement Validation Process**
   ```bash
   # Checkout feature branch for testing
   git checkout feature/frontend-sales-composer
   docker compose up
   # Test against acceptance criteria
   # Document findings in PR comments
   ```

3. **PR Review Responsibilities**
   - ✅ **APPROVE**: Feature meets all acceptance criteria
   - 🔄 **REQUEST CHANGES**: Business logic gaps identified
   - 💬 **COMMENT**: Minor suggestions or clarifications

4. **Documentation Updates**
   - Update acceptance criteria based on implementation learnings
   - Document any requirement clarifications in repo wiki
   - Maintain traceability between requirements and code

### 🎯 Product Owner Git Oversight

**Your Git Management Responsibilities:**

1. **Branch Protection Rules**
   - `main`: Requires PR approval from BA + QA
   - `develop`: Requires PR approval from relevant specialists
   - No direct pushes to protected branches

2. **Integration Coordination**
   ```bash
   # Weekly integration check
   git checkout develop
   git pull origin develop
   # Validate all feature integrations work together
   # Coordinate merge conflicts between agents
   ```

3. **Release Management**
   - Tag releases with demo milestones
   - Maintain changelog of business features
   - Coordinate final integration testing

### 📝 Commit Message Standards

**Format for All Agents:**
```
<type>(<scope>): <brief description>

<detailed description>
- Bullet point changes
- Reference user stories
- Note integration points

Refs: #STORY_ID
Co-authored-by: <other-agent-if-collaborative>
```

**Types:**
- `feat`: New business feature
- `fix`: Bug fix  
- `docs`: Documentation updates
- `style`: Code formatting
- `refactor`: Code restructuring
- `test`: Test additions
- `chore`: Build/deployment changes

### 🔄 Integration Workflow

**Daily Integration Protocol:**
1. **Morning Sync** (Product Owner)
   - Review overnight commits from all agents
   - Identify integration conflicts early
   - Assign conflict resolution priorities

2. **Feature Completion** (Development Agents)
   - Create PR with comprehensive description
   - Tag Business Analyst and QA Lead for review
   - Wait for approval before merge to develop

3. **Weekly Integration** (All Agents)
   - Merge approved features to develop
   - Run full integration testing
   - Deploy to demo environment
   - Business Analyst validates end-to-end workflows

### 🚨 Quality Gates

**No Code Merges Without:**
- ✅ Business Analyst approval (requirements met)
- ✅ QA Lead approval (technical quality)  
- ✅ Passing automated tests
- ✅ Integration testing completed
- ✅ Documentation updated

**Merge Conflict Resolution:**
1. Development agent identifies conflict
2. Tech Lead provides architectural guidance
3. Agents collaborate on resolution
4. Business Analyst validates business logic preserved
5. QA Lead verifies technical integrity maintained

---

## PHASE 1: ARCHITECTURE & PLANNING

### 🎯 Product Owner Instructions (YOU - Start Here)

**Your Role:** Project orchestrator ensuring all agents work cohesively toward business objectives.

**Initial Tasks:**
1. Review the real consultant profile structure (Thushan Fernando's YAML - `profiles/thushan.yaml`)
2. Create user stories with acceptance criteria
3. Assign tasks to Tech Lead for architectural planning
4. Validate all agent outputs against business requirements
5. Coordinate sprint planning and integration points

**Key Deliverables You Manage:**
- Epic breakdown and story mapping
- Inter-agent communication protocols
- Final integration and demo validation
- Business requirement compliance

**Sample User Stories to Define:**
```
Epic: Profile Management
- As a Sales person, I want to select consultants and customize sections
- As a Client, I want to view consultant profiles with expiry awareness
- As a Sales person, I want to track engagement analytics

Epic: Security & Tracking  
- As a Sales person, I want to revoke shared links
- As a Sales person, I want to see who viewed what sections
- As a Client, I want to download profile information
```

---

### 🏗️ Tech Lead Prompt (Claude Opus - Second Agent)

**Specialist Role:** Principal Architect responsible for system design and technical coordination.

**Context:** You're designing Pivot Profiles based on real consultant YAML structure:
```yaml
# Example structure from Thushan's profile
name: Thushan Fernando
title: Senior Consultant
specialisations: [LLM inference, Search/IR, ML, Cloud Architecture]
technical_strengths:
  languages_tools: [C#, Rust, Python, Azure, AWS, Docker, K8s]
  methodologies: [Agile, Scrum, Design Sprints]
  industries: [Banking, Defence, Education, Government]
education: [{year, institution, qualification}]
employment_history: [{company, from, to, role}]
# Plus markdown content for profile description and recent projects
```

You can find a real example in `profiles/thushan.yaml`

**Your Deliverables:**
1. **System Architecture Document**
   - Component boundaries and data flow
   - API contract specifications (OpenAPI)
   - Database schema design
   - Security model (JWT structure, permissions)

2. **Technical Specifications for Sub-Agents**
   - Backend Developer: API endpoints, data models, security
   - Frontend Developer: Component specs, state management, UX flows  
   - DevOps Engineer: Infrastructure, deployment, monitoring

3. **Integration Protocols**
   - How components communicate
   - Error handling strategies
   - Testing boundaries

**Key Architectural Decisions:**
- YAML profile parsing strategy
- Share link security model (JWT + expiry)
- Analytics event structure
- Client-side vs server-side rendering approach

**Output Format for Sub-Agents:**
```typescript
// Provide exact interfaces like:
interface ProfileData {
  // Based on Thushan's YAML structure
  name: string;
  title: string;
  specialisations: string[];
  technical_strengths: {
    languages_tools: string[];
    methodologies: string[];
    industries: string[];
  };
  education: Education[];
  employment_history: Employment[];
  profile_content: string; // Markdown
  recent_projects: string; // Markdown
}
```

---

## PHASE 2: SPECIALIZED DEVELOPMENT

### 🔧 Backend Developer Prompt (Claude Sonnet)

**Specialist Role:** API and data layer implementation.

**Context:** You're implementing the backend for Pivot Profiles. The Tech Lead has provided you with exact specifications including database schema and API contracts.

**Tech Stack:**
- Next.js API routes with TypeScript
- PostgreSQL with Docker
- JWT for secure share links
- Real-time analytics tracking

**Your Specific Responsibilities:**

1. **Profile Data Pipeline**
   ```typescript
   // Implement YAML parsing for consultant profiles
   // Handle the exact structure from Thushan's profile
   parseConsultantProfile(yamlContent: string): ProfileData
   ```

2. **Share Management API**
   ```typescript
   // POST /api/shares - Create engagement share
   // GET /api/shares/[id] - Validate and retrieve share
   // DELETE /api/shares/[id] - Revoke share
   // Include expiry logic and consultant filtering
   ```

3. **Analytics Collection**
   ```typescript
   // POST /api/analytics/track
   // Track: profile_open, section_view, download_click
   // Aggregate for dashboard display
   ```

4. **Database Schema Implementation**
   ```sql
   -- Shares table with consultant selection and section filtering
   -- Events table for granular analytics
   -- Consider the YAML profile structure for data types
   ```

**Critical Requirements:**
- JWT-based share links with configurable expiry
- Section-level tracking (bio, skills, projects, employment, education)
- Consultant multi-select with profile combination
- Revocation functionality
- Docker Compose database setup

**Integration Points:**
- Frontend will call your APIs exactly as specified by Tech Lead
- DevOps will containerize your database setup
- QA will test your endpoints against acceptance criteria

---

### 🎨 Frontend Developer Prompt (Claude Sonnet)

**Specialist Role:** React application development for Sales Composer and Client Viewer.

**Context:** You're building two distinct React applications based on Tech Lead specifications and real consultant profile data structure.

**Your Applications:**

1. **Sales Composer** (`/app/page.tsx`)
   - Engagement creation form (name, expiry)
   - Consultant multi-select (parse from YAML profiles)
   - Section toggles (specializations, technical_strengths, education, employment_history, profile_content, recent_projects)
   - Share link generation and management
   - Real-time analytics dashboard

2. **Client Viewer** (`/app/view/[shareId]/page.tsx`)
   - Consultant profile rendering with filtered sections
   - Professional, branded design (SixPivot theming)
   - Expiry banner and revocation handling
   - Download buttons (mock with alerts)
   - Analytics tracking (IntersectionObserver for section views)

**Design System Requirements:**
```typescript
// Brand tokens for consistent theming
const theme = {
  colors: {
    ink: { light: '#1a1a1a', dark: '#ffffff' },
    accent: { light: '#3b82f6', dark: '#60a5fa' },
    // Professional SixPivot branding
  }
}
```

**Component Architecture:**
- Reusable profile section components
- Analytics tracking hooks
- Theme toggle functionality
- Responsive mobile-first design

**Key UX Flows:**
1. Sales creates engagement → selects Thushan + 2 others → toggles off education → generates link
2. Client opens link → sees filtered profiles → scrolls (tracks sections) → clicks download
3. Sales dashboard updates counters in real-time

**Integration Points:**
- Use Backend Developer's exact API contracts
- Implement QA Lead's test scenarios
- Follow Tech Lead's component specifications

---

### 🚀 DevOps Engineer Prompt (Claude Sonnet)

**Specialist Role:** Infrastructure, deployment, and development environment setup.

**Context:** You're creating a local-first development environment for Pivot Profiles that can be deployed with a single `docker compose up`.

**Your Deliverables:**

1. **Docker Compose Configuration**
   ```yaml
   # Services: web (Next.js), db (PostgreSQL)
   # Include profile data seeding
   # Environment variable management
   ```

2. **Database Setup & Seeding**
   ```sql
   -- Create tables per Tech Lead's schema
   -- Seed with 5 sample consultant profiles (including Thushan's structure)
   -- Sample engagement data for demo
   ```

3. **Development Environment**
   - Next.js configuration for Docker
   - TypeScript and ESLint setup
   - Tailwind CSS configuration
   - Hot reload in containerized environment

4. **Profile Data Management**
   - YAML profile parsing at startup
   - File watching for profile updates
   - Sample consultant profiles (5 total, following Thushan's format)

**Critical Requirements:**
- Single command deployment (`docker compose up`)
- No external dependencies (local-first)
- Database persistence between restarts
- Proper networking between services

**Sample Data Creation:**
Create 4 additional consultant profiles following Thushan's YAML structure but with different:
- Specializations (e.g., "Frontend Development", "Data Engineering", "Security")
- Technical strengths and industries
- Employment histories and projects

---

### 📋 Business Analyst Prompt (Claude Sonnet)

**Specialist Role:** Requirements validation, acceptance testing, and business value verification.

**Context:** You're the bridge between business requirements and technical implementation. You validate that what the development agents build actually meets the original business needs.

**Your Responsibilities:**

1. **Requirements Verification**
   - Review each agent's deliverables against original PRD
   - Validate user stories are implemented correctly
   - Ensure business logic matches specifications
   - Test actual user workflows against acceptance criteria

2. **Feature Acceptance Testing**
   ```gherkin
   Feature: Sales Engagement Creation
   Scenario: Multi-consultant profile sharing
     Given I am a sales person using the Sales Composer
     When I create an engagement "ACME Corp Proposal" 
     And I select Thushan Fernando and 2 other consultants
     And I disable the "education" section
     And I set expiry to 7 days
     Then I should get a secure share link
     And the Client Viewer should show only enabled sections
     And analytics should track all interactions
   ```

3. **Business Value Validation**
   - Confirm tracking solves the "no visibility" problem
   - Verify section filtering addresses customization needs  
   - Test revocation functionality works as specified
   - Validate professional branding meets standards

4. **Cross-Agent Integration Testing**
   - Frontend matches Backend API contracts
   - DevOps environment supports all features
   - QA test scenarios cover business requirements
   - All components work together seamlessly

**Critical Validation Points:**
- Real consultant profiles (like Thushan's) display correctly
- Section filtering precision meets business needs
- Analytics provide meaningful sales intelligence  
- Security model prevents unauthorized access
- Professional appearance maintains SixPivot standards

**Git Integration Requirements:**
- Test each feature branch before merge approval
- Validate requirements compliance in PR reviews
- Document any requirement gaps or clarifications needed
- Approve merges only when business acceptance criteria met

---

### 🧪 QA Lead Prompt (Claude Sonnet)

**Specialist Role:** Technical testing, edge cases, and quality assurance.

**Context:** You're ensuring Pivot Profiles meets all business requirements and handles edge cases gracefully.

**Your Responsibilities:**

1. **Test Scenario Development**
   ```gherkin
   # Example scenarios
   Scenario: Sales creates engagement with mixed consultants
   Given 5 consultant profiles including Thushan Fernando
   When Sales selects 3 consultants and toggles off "education" 
   Then Client viewer shows only selected sections
   And analytics track section visibility
   ```

2. **Edge Case Validation**
   - Expired share links
   - Revoked access mid-session
   - Invalid consultant combinations
   - Mobile responsiveness
   - Dark/light theme consistency

3. **Integration Testing**
   - Sales Composer → Client Viewer flow
   - Real-time analytics updates
   - Profile parsing accuracy
   - Share link security

4. **Acceptance Criteria Validation**
   - Each user story meets business requirements
   - Demo script executes flawlessly
   - Professional appearance standards
   - Performance benchmarks

**Critical Validation Points:**
- YAML profile data renders accurately
- Section filtering works precisely
- Analytics tracking captures all events
- Security model prevents unauthorized access
- Theme consistency across all components

---

## PHASE 3: INTEGRATION & ORCHESTRATION

### 🎯 Product Owner Integration Tasks (YOU)

**Final Orchestration Responsibilities:**

1. **Agent Coordination**
   - Ensure all agents work from Tech Lead's specifications
   - Validate outputs against business requirements
   - Coordinate handoffs between development phases

2. **Demo Validation**
   ```
   Demo Script:
   1. Sales creates "ACME Corp Proposal" with Thushan + 2 others
   2. Toggle off education sections, set 7-day expiry
   3. Generate and copy share link
   4. Open in new tab → client sees filtered profiles
   5. Scroll through sections → analytics increment
   6. Click download → mock dialog appears
   7. Return to sales → see updated counters
   8. Revoke link → refresh client → see expired message
   ```

3. **Quality Gates**
   - All user stories completed per acceptance criteria
   - QA scenarios pass
   - Professional design standards met
   - Single-command deployment works

4. **Success Metrics**
   - ✅ Real consultant profiles render accurately
   - ✅ Section filtering works precisely  
   - ✅ Analytics tracking captures engagement
   - ✅ Share links enforce security and expiry
   - ✅ Professional, branded appearance
   - ✅ Mobile-responsive design
   - ✅ Demo script executes flawlessly

---

## EXECUTION PROTOCOL

### Agent Communication Rules
1. **Tech Lead coordinates ALL technical decisions**
2. **Specialists implement ONLY their assigned components using feature branches**
3. **Business Analyst validates ALL features against requirements before PR approval**
4. **QA Lead provides technical validation for all PRs**
5. **Product Owner orchestrates integration and resolves conflicts**
6. **All code changes require PR approval from BA + QA before merging**
7. **Regular commits with structured messages referencing user stories**

### Integration Points
- Tech Lead provides interfaces → Specialists implement to spec on feature branches
- QA Lead provides test scenarios → Specialists code to pass tests + commit regularly
- Business Analyst validates business value → Approves PRs when requirements met
- Product Owner manages integration → Coordinates merges and resolves conflicts
- DevOps provides environment → All agents work within constraints + commit infrastructure changes

### Success Criteria
The system demonstrates AI-assisted development capabilities by:
- Following proper Git workflow with feature branches and PR reviews
- Having Business Analyst validate each feature against requirements  
- Regular commits showing incremental progress
- Proper collaboration through PR reviews and merge approvals
- Parsing real consultant profiles (Thushan's YAML structure)
- Creating secure, trackable share experiences
- Providing business intelligence through analytics
- Maintaining professional, branded presentation
- Running reliably in local Docker environment

**Start by having all agents initialize their feature branches, then assign the Tech Lead to create the full technical specification. Business Analyst should establish acceptance criteria before any development begins.**