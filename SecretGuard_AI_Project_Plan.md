# SecretGuard AI Platform - Complete Project Plan

## Executive Summary

**Project Name:** SecretGuard AI Platform  
**Duration:** 16-20 weeks  
**Team Size:** 1-3 engineers (can be scaled)  
**Budget Estimate:** $5,000-$15,000 (cloud infrastructure + AI API costs)

**Objective:** Build an enterprise-grade automated secret scanning platform that continuously monitors GitHub repositories, uses AI for intelligent analysis and prioritization, stores findings in a knowledge graph, and provides actionable insights through multiple interfaces.

**Key Differentiators:**
- AI-powered risk assessment and classification
- Natural language query interface
- Knowledge graph for relationship analysis
- Predictive analytics for proactive scanning
- Behavioral anomaly detection
- Automated report generation

---

## Table of Contents

1. [Project Phases](#project-phases)
2. [Phase 1: Foundation & Core Infrastructure](#phase-1-foundation--core-infrastructure-weeks-1-4)
3. [Phase 2: AI Integration](#phase-2-ai-integration-weeks-5-8)
4. [Phase 3: Graph Database & Analytics](#phase-3-graph-database--analytics-weeks-9-10)
5. [Phase 4: API & Dashboard](#phase-4-api--dashboard-weeks-11-13)
6. [Phase 5: Notifications & Reporting](#phase-5-notifications--reporting-week-14)
7. [Phase 6: Testing & Deployment](#phase-6-testing--deployment-weeks-15-16)
8. [Resource Requirements](#resource-requirements)
9. [Timeline & Milestones](#timeline--milestones)
10. [Risk Assessment & Mitigation](#risk-assessment--mitigation)
11. [Success Metrics](#success-metrics)
12. [Documentation Requirements](#documentation-requirements)
13. [Post-Launch Plan](#post-launch-plan)

---

## Project Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        SecretGuard AI Platform                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌──────────────┐      ┌──────────────┐      ┌──────────────┐  │
│  │   GitHub     │─────▶│   Scanner    │─────▶│    Neo4j     │  │
│  │     API      │      │ Orchestrator │      │    Graph     │  │
│  └──────────────┘      └──────────────┘      └──────────────┘  │
│                               │                       │          │
│                               ▼                       ▼          │
│                        ┌──────────────┐      ┌──────────────┐  │
│                        │  TruffleHog  │      │  PostgreSQL  │  │
│                        │   Scanner    │      │    Queue     │  │
│                        └──────────────┘      └──────────────┘  │
│                               │                       │          │
│                               ▼                       ▼          │
│                        ┌──────────────────────────────────┐    │
│                        │      AI Analysis Layer           │    │
│                        │  ┌────────────────────────────┐  │    │
│                        │  │   Claude API (Anthropic)   │  │    │
│                        │  │  - Secret Classification   │  │    │
│                        │  │  - Natural Language Query  │  │    │
│                        │  │  - Similarity Detection    │  │    │
│                        │  │  - Behavior Analysis       │  │    │
│                        │  │  - Report Generation       │  │    │
│                        │  └────────────────────────────┘  │    │
│                        └──────────────────────────────────┘    │
│                                      │                          │
│                                      ▼                          │
│                        ┌──────────────────────────────────┐    │
│                        │      User Interfaces             │    │
│                        │  ┌────────────────────────────┐  │    │
│                        │  │   Web Dashboard (React)    │  │    │
│                        │  │   REST/GraphQL API         │  │    │
│                        │  │   Neo4j Browser            │  │    │
│                        │  │   Slack/Email/PagerDuty    │  │    │
│                        │  └────────────────────────────┘  │    │
│                        └──────────────────────────────────┘    │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

## Phase 1: Foundation & Core Infrastructure (Weeks 1-4)

### Week 1: Project Setup & Architecture

**Deliverables:**
- [ ] Project repository structure
- [ ] Development environment setup
- [ ] CI/CD pipeline (GitHub Actions)
- [ ] Docker containerization
- [ ] Architecture documentation

**Project Structure:**
```
secretguard/
├── scanner/                 # TruffleHog orchestration
│   ├── __init__.py
│   ├── repo_enumerator.py
│   ├── scan_orchestrator.py
│   ├── trufflehog_wrapper.py
│   ├── prioritizer.py
│   └── queue_manager.py
├── ai/                      # AI analysis modules
│   ├── __init__.py
│   ├── secret_analyzer.py
│   ├── query_agent.py
│   ├── similarity_detector.py
│   ├── behavior_analyzer.py
│   └── report_generator.py
├── graph/                   # Neo4j integration
│   ├── __init__.py
│   ├── schema.py
│   ├── ingestion.py
│   ├── queries.py
│   └── access_manager.py
├── api/                     # REST/GraphQL APIs
│   ├── __init__.py
│   ├── rest_api.py
│   ├── graphql_schema.py
│   ├── auth.py
│   └── websocket_server.py
├── dashboard/               # Web UI
│   ├── frontend/
│   │   ├── src/
│   │   ├── public/
│   │   ├── package.json
│   │   └── vite.config.ts
│   └── backend/
│       └── server.py
├── notifications/           # Alert system
│   ├── __init__.py
│   ├── slack.py
│   ├── email.py
│   └── pagerduty.py
├── config/                  # Configuration
│   ├── config.yaml
│   ├── secrets.env.example
│   └── logging.yaml
├── tests/                   # Test suite
│   ├── unit/
│   ├── integration/
│   ├── e2e/
│   └── performance/
├── docs/                    # Documentation
│   ├── architecture.md
│   ├── api.md
│   ├── deployment.md
│   └── user_guide.md
├── scripts/                 # Utility scripts
│   ├── setup_db.py
│   ├── migrate.py
│   └── seed_data.py
├── docker-compose.yml
├── docker-compose.prod.yml
├── Dockerfile
├── requirements.txt
├── .env.example
├── .gitignore
├── README.md
└── LICENSE
```

**Technical Stack:**
- **Language:** Python 3.11+
- **Graph Database:** Neo4j 5.x
- **Relational Database:** PostgreSQL 15
- **AI:** Anthropic Claude API (Sonnet 4)
- **Frontend:** React 18 + TypeScript
- **API Framework:** FastAPI
- **Container:** Docker + Docker Compose
- **CI/CD:** GitHub Actions
- **Secret Scanner:** TruffleHog

**Setup Commands:**
```bash
# Clone repository
git clone <your-repo-url>
cd secretguard

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Copy environment file
cp .env.example .env
# Edit .env with your credentials

# Start databases
docker-compose up -d neo4j postgres

# Initialize databases
python scripts/setup_db.py

# Run tests
pytest
```

---

### Week 2: Database & Data Models

**Deliverables:**
- [ ] Neo4j schema definition
- [ ] PostgreSQL queue schema
- [ ] Data migration scripts
- [ ] Database access layer

#### Neo4j Schema

**Node Types:**
```cypher
// Repository Node
CREATE CONSTRAINT repo_name IF NOT EXISTS 
FOR (r:Repository) REQUIRE r.name IS UNIQUE;

// Properties: name, organization, url, visibility, size, language, 
//            last_scanned, created_at, updated_at

// Commit Node
CREATE CONSTRAINT commit_hash IF NOT EXISTS 
FOR (c:Commit) REQUIRE c.hash IS UNIQUE;

// Properties: hash, author, timestamp, message, branch

// SecretFinding Node
CREATE CONSTRAINT secret_id IF NOT EXISTS 
FOR (s:SecretFinding) REQUIRE s.id IS UNIQUE;

// Properties: id, secret_type, verified, severity, status, file_path,
//            line_number, first_detected, remediated_at, code_context,
//            ai_severity, ai_confidence, ai_reasoning, ai_exposure_scope,
//            ai_blast_radius, ai_fp_likelihood

// Developer Node
CREATE CONSTRAINT developer_email IF NOT EXISTS 
FOR (d:Developer) REQUIRE d.email IS UNIQUE;

// Properties: email, username, name

// Team Node
CREATE CONSTRAINT team_name IF NOT EXISTS 
FOR (t:Team) REQUIRE t.name IS UNIQUE;

// Properties: name, description

// RemediationAction Node
// Properties: description, status, created_at, completed_at, assigned_to
```

**Indexes for Performance:**
```cypher
CREATE INDEX repo_org IF NOT EXISTS 
FOR (r:Repository) ON (r.organization);

CREATE INDEX secret_type IF NOT EXISTS 
FOR (s:SecretFinding) ON (s.secret_type);

CREATE INDEX secret_status IF NOT EXISTS 
FOR (s:SecretFinding) ON (s.status);

CREATE INDEX secret_verified IF NOT EXISTS 
FOR (s:SecretFinding) ON (s.verified);

CREATE INDEX secret_severity IF NOT EXISTS 
FOR (s:SecretFinding) ON (s.severity);

CREATE INDEX commit_timestamp IF NOT EXISTS 
FOR (c:Commit) ON (c.timestamp);

CREATE INDEX secret_first_detected IF NOT EXISTS 
FOR (s:SecretFinding) ON (s.first_detected);
```

**Relationships:**
```cypher
// Repository to Commit
(Repository)-[:HAS_COMMIT]->(Commit)

// Commit to Secret
(Commit)-[:CONTAINS_SECRET]->(SecretFinding)

// Developer to Commit
(Developer)-[:AUTHORED]->(Commit)

// Developer to Team
(Developer)-[:MEMBER_OF]->(Team)

// Team to Repository
(Team)-[:OWNS]->(Repository)

// Secret to Secret (similarity)
(SecretFinding)-[:SIMILAR_TO]->(SecretFinding)

// Secret to Action
(SecretFinding)-[:REQUIRES_ACTION]->(RemediationAction)

// Developer to Action
(Developer)-[:ASSIGNED_TO]->(RemediationAction)
```

#### PostgreSQL Schema

```sql
-- Scan Queue Table
CREATE TABLE scan_queue (
    id SERIAL PRIMARY KEY,
    repo_name TEXT UNIQUE NOT NULL,
    repo_url TEXT NOT NULL,
    organization TEXT,
    priority_score INTEGER DEFAULT 0,
    risk_score FLOAT,
    status TEXT DEFAULT 'pending' 
        CHECK (status IN ('pending', 'scanning', 'completed', 'failed')),
    last_scanned_at TIMESTAMPTZ,
    last_scanned_commit TEXT,
    scan_duration_seconds INTEGER,
    secrets_found INTEGER DEFAULT 0,
    verified_secrets_found INTEGER DEFAULT 0,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW(),
    retry_count INTEGER DEFAULT 0,
    error_message TEXT,
    metadata JSONB
);

CREATE INDEX idx_status_priority ON scan_queue(status, priority_score DESC);
CREATE INDEX idx_last_scanned ON scan_queue(last_scanned_at NULLS FIRST);
CREATE INDEX idx_organization ON scan_queue(organization);
CREATE INDEX idx_repo_name ON scan_queue(repo_name);

-- Scan History Table
CREATE TABLE scan_history (
    id SERIAL PRIMARY KEY,
    repo_name TEXT NOT NULL,
    scan_started_at TIMESTAMPTZ NOT NULL,
    scan_completed_at TIMESTAMPTZ,
    commit_hash TEXT,
    secrets_found INTEGER,
    verified_secrets INTEGER,
    status TEXT,
    duration_seconds INTEGER,
    scanner_version TEXT,
    metadata JSONB
);

CREATE INDEX idx_scan_history_repo ON scan_history(repo_name);
CREATE INDEX idx_scan_history_started ON scan_history(scan_started_at DESC);

-- AI Analysis Cache Table
CREATE TABLE ai_analysis_cache (
    id SERIAL PRIMARY KEY,
    secret_finding_id TEXT UNIQUE NOT NULL,
    analysis_result JSONB NOT NULL,
    analyzed_at TIMESTAMPTZ DEFAULT NOW(),
    model_version TEXT,
    cache_hit_count INTEGER DEFAULT 0
);

CREATE INDEX idx_ai_cache_secret ON ai_analysis_cache(secret_finding_id);
CREATE INDEX idx_ai_cache_analyzed ON ai_analysis_cache(analyzed_at DESC);

-- Notification Log Table
CREATE TABLE notification_log (
    id SERIAL PRIMARY KEY,
    secret_finding_id TEXT NOT NULL,
    notification_type TEXT NOT NULL 
        CHECK (notification_type IN ('slack', 'email', 'pagerduty', 'webhook')),
    recipient TEXT NOT NULL,
    sent_at TIMESTAMPTZ DEFAULT NOW(),
    acknowledged_at TIMESTAMPTZ,
    status TEXT DEFAULT 'sent' 
        CHECK (status IN ('sent', 'delivered', 'failed', 'acknowledged')),
    metadata JSONB
);

CREATE INDEX idx_notification_secret ON notification_log(secret_finding_id);
CREATE INDEX idx_notification_sent ON notification_log(sent_at DESC);

-- User Preferences Table
CREATE TABLE user_preferences (
    id SERIAL PRIMARY KEY,
    user_id TEXT UNIQUE NOT NULL,
    email TEXT,
    slack_user_id TEXT,
    notification_settings JSONB,
    query_history JSONB,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- API Keys Table
CREATE TABLE api_keys (
    id SERIAL PRIMARY KEY,
    key_hash TEXT UNIQUE NOT NULL,
    user_id TEXT NOT NULL,
    name TEXT NOT NULL,
    permissions JSONB,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    expires_at TIMESTAMPTZ,
    last_used_at TIMESTAMPTZ,
    active BOOLEAN DEFAULT true
);

CREATE INDEX idx_api_key_hash ON api_keys(key_hash);
CREATE INDEX idx_api_key_user ON api_keys(user_id);
```

---

### Week 3: Repository Enumeration & Prioritization

**Deliverables:**
- [ ] GitHub API integration
- [ ] GraphQL enumeration
- [ ] Risk scoring algorithm
- [ ] Priority queue system

**Implementation Files:**

#### `scanner/repo_enumerator.py`

```python
from github import Github
import requests
from typing import List, Dict, Optional
from datetime import datetime

class RepoEnumerator:
    """Enumerate repositories from GitHub"""
    
    def __init__(self, token: str, org_name: Optional[str] = None):
        self.gh = Github(token)
        self.org_name = org_name
        self.token = token
    
    def enumerate_org_repos(self) -> List[Dict]:
        """Get all repos in an organization"""
        org = self.gh.get_organization(self.org_name)
        repos = []
        
        for repo in org.get_repos(type='all'):
            repos.append(self._extract_repo_metadata(repo))
        
        return repos
    
    def enumerate_user_repos(self) -> List[Dict]:
        """Get all repos user has access to"""
        user = self.gh.get_user()
        repos = []
        
        for repo in user.get_repos():
            repos.append(self._extract_repo_metadata(repo))
        
        return repos
    
    def enumerate_team_repos(self, team_id: int) -> List[Dict]:
        """Get repos owned by specific team"""
        org = self.gh.get_organization(self.org_name)
        team = org.get_team(team_id)
        repos = []
        
        for repo in team.get_repos():
            repos.append(self._extract_repo_metadata(repo))
        
        return repos
    
    def enumerate_with_graphql(self, org: str) -> List[Dict]:
        """More efficient enumeration using GraphQL"""
        query = """
        query($org: String!, $cursor: String) {
          organization(login: $org) {
            repositories(first: 100, after: $cursor) {
              pageInfo {
                hasNextPage
                endCursor
              }
              nodes {
                nameWithOwner
                url
                isPrivate
                diskUsage
                updatedAt
                createdAt
                primaryLanguage { name }
                isArchived
                repositoryTopics(first: 10) {
                  nodes { topic { name } }
                }
                defaultBranchRef {
                  name
                  target {
                    ... on Commit {
                      history(first: 1) {
                        totalCount
                      }
                    }
                  }
                }
              }
            }
          }
        }
        """
        
        headers = {"Authorization": f"Bearer {self.token}"}
        all_repos = []
        cursor = None
        
        while True:
            response = requests.post(
                'https://api.github.com/graphql',
                json={'query': query, 'variables': {'org': org, 'cursor': cursor}},
                headers=headers
            )
            data = response.json()['data']['organization']['repositories']
            all_repos.extend(self._transform_graphql_repos(data['nodes']))
            
            if not data['pageInfo']['hasNextPage']:
                break
            cursor = data['pageInfo']['endCursor']
        
        return all_repos
    
    def _extract_repo_metadata(self, repo) -> Dict:
        """Extract metadata from PyGithub repo object"""
        return {
            'name': repo.full_name,
            'url': repo.clone_url,
            'organization': repo.owner.login,
            'visibility': 'private' if repo.private else 'public',
            'size': repo.size,
            'updated_at': repo.updated_at,
            'created_at': repo.created_at,
            'language': repo.language,
            'archived': repo.archived,
            'topics': repo.get_topics(),
            'default_branch': repo.default_branch,
            'open_issues': repo.open_issues_count,
            'watchers': repo.watchers_count,
            'forks': repo.forks_count,
            'stars': repo.stargazers_count
        }
    
    def _transform_graphql_repos(self, nodes: List[Dict]) -> List[Dict]:
        """Transform GraphQL response to standard format"""
        repos = []
        for node in nodes:
            repos.append({
                'name': node['nameWithOwner'],
                'url': f"https://github.com/{node['nameWithOwner']}.git",
                'organization': node['nameWithOwner'].split('/')[0],
                'visibility': 'private' if node['isPrivate'] else 'public',
                'size': node['diskUsage'],
                'updated_at': datetime.fromisoformat(node['updatedAt'].replace('Z', '+00:00')),
                'created_at': datetime.fromisoformat(node['createdAt'].replace('Z', '+00:00')),
                'language': node['primaryLanguage']['name'] if node['primaryLanguage'] else None,
                'archived': node['isArchived'],
                'topics': [t['topic']['name'] for t in node['repositoryTopics']['nodes']],
                'default_branch': node['defaultBranchRef']['name'] if node['defaultBranchRef'] else 'main',
                'commit_count': node['defaultBranchRef']['target']['history']['totalCount'] if node['defaultBranchRef'] else 0
            })
        return repos
```

#### `scanner/prioritizer.py`

```python
from typing import List, Dict
from datetime import datetime, timedelta

class RepoPrioritizer:
    """Calculate risk scores and prioritize repos"""
    
    def calculate_risk_score(self, repo: Dict) -> float:
        """Higher score = higher priority to scan"""
        score = 0.0
        
        # Recency - recently updated repos more likely to have new secrets
        days_since_update = (datetime.now(repo['updated_at'].tzinfo) - repo['updated_at']).days
        if days_since_update < 7:
            score += 50
        elif days_since_update < 30:
            score += 30
        elif days_since_update < 90:
            score += 10
        
        # Visibility - public repos are higher risk
        if repo['visibility'] == 'public':
            score += 100
        
        # Activity level - more active = more likely to have issues
        score += min(repo.get('open_issues', 0) * 2, 50)
        score += min(repo.get('forks', 0) * 3, 50)
        score += min(repo.get('watchers', 0) * 2, 30)
        
        # Language risk profiles
        risk_languages = {
            'Python': 20, 'JavaScript': 20, 'TypeScript': 15,
            'Ruby': 15, 'PHP': 20, 'Shell': 25, 'Go': 15,
            'Java': 15, 'C#': 15, 'Kotlin': 10
        }
        score += risk_languages.get(repo.get('language'), 10)
        
        # Topics - infrastructure/deployment related
        high_risk_topics = [
            'production', 'infrastructure', 'deployment',
            'aws', 'gcp', 'azure', 'kubernetes', 'terraform',
            'ansible', 'docker', 'ci-cd', 'api', 'backend'
        ]
        matching_topics = set(repo.get('topics', [])) & set(high_risk_topics)
        score += len(matching_topics) * 15
        
        # Repository size (larger repos may have more secrets, but slower to scan)
        if repo['size'] > 100000:  # > 100MB
            score += 10
        elif repo['size'] > 10000:  # > 10MB
            score += 5
        
        # Never scanned before - highest priority
        if not repo.get('last_scanned'):
            score += 200
        else:
            # Time since last scan
            days_since_scan = (datetime.now() - repo['last_scanned']).days
            if days_since_scan > 30:
                score += 30
            elif days_since_scan > 7:
                score += 15
        
        # Commit activity (if available)
        if 'commit_count' in repo:
            if repo['commit_count'] > 1000:
                score += 20
            elif repo['commit_count'] > 100:
                score += 10
        
        return score
    
    def prioritize(self, repos: List[Dict]) -> List[Dict]:
        """Sort repos by risk score"""
        for repo in repos:
            repo['risk_score'] = self.calculate_risk_score(repo)
        
        return sorted(repos, key=lambda r: r['risk_score'], reverse=True)
    
    def filter_archived(self, repos: List[Dict]) -> List[Dict]:
        """Remove archived repos unless they were recently updated"""
        return [
            r for r in repos 
            if not r.get('archived') or 
            (datetime.now(r['updated_at'].tzinfo) - r['updated_at']).days < 90
        ]
    
    def filter_by_language(self, repos: List[Dict], languages: List[str]) -> List[Dict]:
        """Filter repos by programming language"""
        return [r for r in repos if r.get('language') in languages]
    
    def filter_by_topic(self, repos: List[Dict], topics: List[str]) -> List[Dict]:
        """Filter repos by topics"""
        return [
            r for r in repos 
            if any(topic in r.get('topics', []) for topic in topics)
        ]
```

#### `scanner/queue_manager.py`

```python
import psycopg2
from psycopg2.extras import RealDictCursor
from typing import List, Dict, Optional
import json
from datetime import datetime

class ScanQueueManager:
    """Manage scan queue in PostgreSQL"""
    
    def __init__(self, db_url: str):
        self.db_url = db_url
        self.conn = psycopg2.connect(db_url)
    
    def populate_queue(self, repos: List[Dict]):
        """Initial population or update of scan queue"""
        with self.conn.cursor() as cursor:
            for repo in repos:
                cursor.execute("""
                    INSERT INTO scan_queue 
                    (repo_name, repo_url, organization, priority_score, risk_score, metadata)
                    VALUES (%s, %s, %s, %s, %s, %s)
                    ON CONFLICT (repo_name) 
                    DO UPDATE SET 
                        priority_score = EXCLUDED.priority_score,
                        risk_score = EXCLUDED.risk_score,
                        metadata = EXCLUDED.metadata,
                        updated_at = NOW()
                """, (
                    repo['name'],
                    repo['url'],
                    repo['organization'],
                    int(repo['risk_score']),
                    repo['risk_score'],
                    json.dumps(repo)
                ))
            self.conn.commit()
    
    def get_next_repo(self) -> Optional[Dict]:
        """Get highest priority repo to scan (with row locking)"""
        with self.conn.cursor(cursor_factory=RealDictCursor) as cursor:
            cursor.execute("""
                UPDATE scan_queue
                SET status = 'scanning', updated_at = NOW()
                WHERE id = (
                    SELECT id FROM scan_queue
                    WHERE status = 'pending'
                    ORDER BY priority_score DESC, created_at ASC
                    LIMIT 1
                    FOR UPDATE SKIP LOCKED
                )
                RETURNING *
            """)
            result = cursor.fetchone()
            self.conn.commit()
            return dict(result) if result else None
    
    def mark_complete(self, repo_id: int, commit_hash: str, 
                      secrets_found: int, verified_count: int, 
                      duration: int):
        """Mark scan as complete"""
        with self.conn.cursor() as cursor:
            cursor.execute("""
                UPDATE scan_queue
                SET status = 'completed',
                    last_scanned_at = NOW(),
                    last_scanned_commit = %s,
                    secrets_found = %s,
                    verified_secrets_found = %s,
                    scan_duration_seconds = %s,
                    retry_count = 0,
                    error_message = NULL
                WHERE id = %s
            """, (commit_hash, secrets_found, verified_count, duration, repo_id))
            
            # Also log to history
            cursor.execute("""
                INSERT INTO scan_history 
                (repo_name, scan_started_at, scan_completed_at, 
                 commit_hash, secrets_found, verified_secrets, 
                 status, duration_seconds)
                SELECT repo_name, 
                       updated_at - INTERVAL '1 second' * %s,
                       NOW(),
                       %s, %s, %s, 'completed', %s
                FROM scan_queue WHERE id = %s
            """, (duration, commit_hash, secrets_found, verified_count, duration, repo_id))
            
            self.conn.commit()
    
    def mark_failed(self, repo_id: int, error: str):
        """Mark scan as failed, increment retry"""
        with self.conn.cursor() as cursor:
            cursor.execute("""
                UPDATE scan_queue
                SET status = CASE 
                        WHEN retry_count >= 3 THEN 'failed'
                        ELSE 'pending'
                    END,
                    retry_count = retry_count + 1,
                    error_message = %s,
                    updated_at = NOW()
                WHERE id = %s
            """, (error, repo_id))
            self.conn.commit()
    
    def get_queue_stats(self) -> Dict:
        """Get queue statistics"""
        with self.conn.cursor(cursor_factory=RealDictCursor) as cursor:
            cursor.execute("""
                SELECT 
                    COUNT(*) FILTER (WHERE status = 'pending') as pending,
                    COUNT(*) FILTER (WHERE status = 'scanning') as scanning,
                    COUNT(*) FILTER (WHERE status = 'completed') as completed,
                    COUNT(*) FILTER (WHERE status = 'failed') as failed,
                    AVG(scan_duration_seconds) FILTER (WHERE status = 'completed') as avg_duration,
                    SUM(secrets_found) as total_secrets_found
                FROM scan_queue
            """)
            return dict(cursor.fetchone())
    
    def reset_stuck_scans(self, timeout_minutes: int = 30):
        """Reset scans stuck in 'scanning' state"""
        with self.conn.cursor() as cursor:
            cursor.execute("""
                UPDATE scan_queue
                SET status = 'pending',
                    retry_count = retry_count + 1
                WHERE status = 'scanning'
                  AND updated_at < NOW() - INTERVAL '%s minutes'
            """, (timeout_minutes,))
            self.conn.commit()
    
    def close(self):
        """Close database connection"""
        self.conn.close()
```

---

### Week 4: TruffleHog Integration & Scanning

**Deliverables:**
- [ ] TruffleHog wrapper
- [ ] Incremental scanning logic
- [ ] Result parsing
- [ ] Error handling & retry logic

#### `scanner/trufflehog_wrapper.py`

```python
import subprocess
import json
import tempfile
import os
from typing import List, Dict, Optional
from pathlib import Path
import logging

logger = logging.getLogger(__name__)

class TruffleHogScanner:
    """Wrapper for TruffleHog secret scanner"""
    
    def __init__(self, trufflehog_path: str = "trufflehog"):
        self.trufflehog_path = trufflehog_path
        self._verify_installation()
    
    def _verify_installation(self):
        """Verify TruffleHog is installed"""
        try:
            result = subprocess.run(
                [self.trufflehog_path, "--version"],
                capture_output=True,
                text=True
            )
            logger.info(f"TruffleHog version: {result.stdout.strip()}")
        except FileNotFoundError:
            raise RuntimeError(
                "TruffleHog not found. Install with: "
                "brew install trufflehog (macOS) or "
                "docker pull trufflesecurity/trufflehog:latest"
            )
    
    def scan_repo_full(self, repo_url: str, branch: str = "main") -> Dict:
        """Scan entire repository history"""
        cmd = [
            self.trufflehog_path,
            "git",
            repo_url,
            "--branch", branch,
            "--json",
            "--no-update"
        ]
        
        return self._execute_scan(cmd, repo_url)
    
    def scan_repo_incremental(self, repo_url: str, since_commit: str) -> Dict:
        """Scan only commits since last scan"""
        cmd = [
            self.trufflehog_path,
            "git",
            repo_url,
            "--since-commit", since_commit,
            "--json",
            "--no-update"
        ]
        
        return self._execute_scan(cmd, repo_url)
    
    def scan_with_verification(self, repo_url: str, since_commit: Optional[str] = None) -> Dict:
        """Scan with verification enabled (only verified secrets)"""
        cmd = [
            self.trufflehog_path,
            "git",
            repo_url,
            "--only-verified",
            "--json",
            "--no-update"
        ]
        
        if since_commit:
            cmd.extend(["--since-commit", since_commit])
        
        return self._execute_scan(cmd, repo_url)
    
    def scan_without_verification(self, repo_url: str, since_commit: Optional[str] = None) -> Dict:
        """Scan without verification (all potential secrets)"""
        cmd = [
            self.trufflehog_path,
            "git",
            repo_url,
            "--json",
            "--no-update"
        ]
        
        if since_commit:
            cmd.extend(["--since-commit", since_commit])
        
        return self._execute_scan(cmd, repo_url)
    
    def _execute_scan(self, cmd: List[str], repo_url: str) -> Dict:
        """Execute TruffleHog scan command"""
        logger.info(f"Starting scan: {' '.join(cmd)}")
        
        try:
            result = subprocess.run(
                cmd,
                capture_output=True,
                text=True,
                timeout=3600  # 1 hour timeout
            )
            
            findings = self.parse_results(result.stdout)
            
            return {
                'repo_url': repo_url,
                'findings': findings,
                'total_found': len(findings),
                'verified_count': sum(1 for f in findings if f.get('verified')),
                'exit_code': result.returncode,
                'stderr': result.stderr if result.returncode != 0 else None
            }
            
        except subprocess.TimeoutExpired:
            logger.error(f"Scan timeout for {repo_url}")
            raise
        except Exception as e:
            logger.error(f"Scan failed for {repo_url}: {e}")
            raise
    
    def parse_results(self, raw_output: str) -> List[Dict]:
        """Parse TruffleHog JSON output"""
        findings = []
        
        for line in raw_output.strip().split('\n'):
            if not line:
                continue
            
            try:
                finding = json.loads(line)
                parsed = self._parse_finding(finding)
                if parsed:
                    findings.append(parsed)
            except json.JSONDecodeError as e:
                logger.warning(f"Failed to parse line: {line[:100]}... Error: {e}")
        
        return findings
    
    def _parse_finding(self, raw_finding: Dict) -> Optional[Dict]:
        """Parse individual finding"""
        try:
            source_metadata = raw_finding.get('SourceMetadata', {}).get('Data', {}).get('Git', {})
            
            return {
                'id': self._generate_finding_id(raw_finding),
                'secret_type': raw_finding.get('DetectorName', 'Unknown'),
                'verified': raw_finding.get('Verified', False),
                'raw_secret': raw_finding.get('Raw', ''),  # Be careful with this
                'commit_hash': source_metadata.get('commit', ''),
                'commit_message': source_metadata.get('message', ''),
                'commit_time': source_metadata.get('timestamp', ''),
                'author': source_metadata.get('email', ''),
                'file_path': source_metadata.get('file', ''),
                'line_number': source_metadata.get('line', 0),
                'repo_url': source_metadata.get('repository', ''),
                'branch': raw_finding.get('SourceMetadata', {}).get('Data', {}).get('Git', {}).get('branch', ''),
            }
        except Exception as e:
            logger.error(f"Error parsing finding: {e}")
            return None
    
    def _generate_finding_id(self, finding: Dict) -> str:
        """Generate unique ID for finding"""
        import hashlib
        
        source = finding.get('SourceMetadata', {}).get('Data', {}).get('Git', {})
        unique_string = f"{source.get('repository')}:{source.get('commit')}:{source.get('file')}:{source.get('line')}"
        
        return hashlib.sha256(unique_string.encode()).hexdigest()[:16]
    
    def extract_code_context(self, repo_path: str, file_path: str, 
                           line_num: int, context_lines: int = 5) -> str:
        """Extract code context around the secret"""
        try:
            full_path = Path(repo_path) / file_path
            with open(full_path, 'r', encoding='utf-8', errors='ignore') as f:
                lines = f.readlines()
            
            start = max(0, line_num - context_lines - 1)
            end = min(len(lines), line_num + context_lines)
            
            context = ''.join(lines[start:end])
            return context
        except Exception as e:
            logger.warning(f"Could not extract context: {e}")
            return ""
```

#### `scanner/scan_orchestrator.py`

```python
import time
import logging
from typing import Dict, List, Optional
from datetime import datetime

from scanner.repo_enumerator import RepoEnumerator
from scanner.prioritizer import RepoPrioritizer
from scanner.queue_manager import ScanQueueManager
from scanner.trufflehog_wrapper import TruffleHogScanner
from graph.ingestion import GraphIngestionPipeline
from ai.secret_analyzer import AISecretAnalyzer

logger = logging.getLogger(__name__)

class ScanOrchestrator:
    """Orchestrate the scanning workflow"""
    
    def __init__(self, config: Dict):
        self.config = config
        
        # Initialize components
        self.enumerator = RepoEnumerator(
            token=config['github_token'],
            org_name=config.get('github_org')
        )
        self.prioritizer = RepoPrioritizer()
        self.queue_manager = ScanQueueManager(config['postgres_url'])
        self.scanner = TruffleHogScanner()
        self.graph = GraphIngestionPipeline(config['neo4j_driver'])
        
        if config.get('enable_ai'):
            self.ai_analyzer = AISecretAnalyzer(config['anthropic_api_key'])
        else:
            self.ai_analyzer = None
    
    def initialize_queue(self):
        """Enumerate repos and populate scan queue"""
        logger.info("Enumerating repositories...")
        
        if self.config.get('github_org'):
            repos = self.enumerator.enumerate_org_repos()
        else:
            repos = self.enumerator.enumerate_user_repos()
        
        logger.info(f"Found {len(repos)} repositories")
        
        # Prioritize
        repos = self.prioritizer.prioritize(repos)
        
        # Populate queue
        self.queue_manager.populate_queue(repos)
        
        logger.info("Queue initialized")
    
    def run_scan_cycle(self, max_scans: Optional[int] = None):
        """Run a scan cycle"""
        scans_completed = 0
        
        while True:
            if max_scans and scans_completed >= max_scans:
                break
            
            # Get next repo from queue
            repo = self.queue_manager.get_next_repo()
            if not repo:
                logger.info("No more repos to scan")
                break
            
            logger.info(f"Scanning {repo['repo_name']} (priority: {repo['priority_score']})")
            
            try:
                # Perform scan
                start_time = time.time()
                results = self._scan_repository(repo)
                duration = int(time.time() - start_time)
                
                # Process results
                self.process_scan_results(results, repo)
                
                # Mark complete
                self.queue_manager.mark_complete(
                    repo['id'],
                    results.get('last_commit', ''),
                    results['total_found'],
                    results['verified_count'],
                    duration
                )
                
                scans_completed += 1
                logger.info(
                    f"Scan complete: {results['total_found']} secrets found "
                    f"({results['verified_count']} verified) in {duration}s"
                )
                
            except Exception as e:
                logger.error(f"Scan failed for {repo['repo_name']}: {e}")
                self.queue_manager.mark_failed(repo['id'], str(e))
    
    def _scan_repository(self, repo: Dict) -> Dict:
        """Scan a single repository"""
        # Determine if incremental or full scan
        if repo.get('last_scanned_commit'):
            results = self.scanner.scan_repo_incremental(
                repo['repo_url'],
                repo['last_scanned_commit']
            )
        else:
            results = self.scanner.scan_repo_full(repo['repo_url'])
        
        return results
    
    def process_scan_results(self, results: Dict, repo_info: Dict):
        """Process scan results: ingest to graph, run AI analysis"""
        findings = results['findings']
        
        if not findings:
            logger.info("No secrets found")
            return
        
        # Ingest to Neo4j
        self.graph.ingest_scan_results(findings, repo_info)
        
        # AI analysis (if enabled)
        if self.ai_analyzer:
            logger.info(f"Running AI analysis on {len(findings)} findings...")
            
            # Batch analysis for efficiency
            analyses = self.ai_analyzer.batch_analyze(findings)
            
            # Update graph with AI insights
            for finding, analysis in zip(findings, analyses):
                self.graph.enrich_with_ai_analysis(finding['id'], analysis)
    
    def continuous_scan(self, interval_seconds: int = 3600):
        """Run continuous scanning with specified interval"""
        while True:
            logger.info("Starting scan cycle...")
            self.run_scan_cycle()
            
            logger.info(f"Cycle complete. Sleeping for {interval_seconds}s")
            time.sleep(interval_seconds)
            
            # Refresh priorities
            self.initialize_queue()
```

---

## Phase 2: AI Integration (Weeks 5-8)

### Week 5: Secret Analysis & Classification

**Deliverables:**
- [ ] AI secret analyzer
- [ ] Context extraction
- [ ] Batch processing
- [ ] Result caching

#### `ai/secret_analyzer.py`

```python
from anthropic import Anthropic
import json
import hashlib
from typing import Dict, List, Optional
import logging

logger = logging.getLogger(__name__)

class AISecretAnalyzer:
    """AI-powered secret analysis using Claude"""
    
    def __init__(self, api_key: str, model: str = "claude-sonnet-4-20250514"):
        self.client = Anthropic(api_key=api_key)
        self.model = model
        self.cache = AIAnalysisCache()
    
    def analyze_secret(self, finding: Dict) -> Dict:
        """Analyze single secret with caching"""
        cache_key = self._generate_cache_key(finding)
        
        if cached := self.cache.get(cache_key):
            logger.debug(f"Cache hit for {finding['id']}")
            return cached
        
        analysis = self._perform_analysis(finding)
        self.cache.set(cache_key, analysis)
        
        return analysis
    
    def batch_analyze(self, findings: List[Dict], batch_size: int = 10) -> List[Dict]:
        """Efficient batch processing"""
        results = []
        
        for i in range(0, len(findings), batch_size):
            batch = findings[i:i+batch_size]
            logger.info(f"Analyzing batch {i//batch_size + 1} ({len(batch)} findings)")
            
            try:
                batch_results = self._analyze_batch(batch)
                results.extend(batch_results)
            except Exception as e:
                logger.error(f"Batch analysis failed: {e}")
                # Fall back to individual analysis
                for finding in batch:
                    try:
                        results.append(self.analyze_secret(finding))
                    except:
                        results.append(self._get_default_analysis())
        
        return results
    
    def _perform_analysis(self, finding: Dict) -> Dict:
        """Perform AI analysis on single secret"""
        prompt = self._build_analysis_prompt(finding)
        
        try:
            response = self.client.messages.create(
                model=self.model,
                max_tokens=1500,
                temperature=0.0,  # Deterministic
                messages=[{"role": "user", "content": prompt}]
            )
            
            analysis = json.loads(response.content[0].text)
            analysis['model_version'] = self.model
            
            return analysis
            
        except Exception as e:
            logger.error(f"AI analysis failed: {e}")
            return self._get_default_analysis()
    
    def _analyze_batch(self, findings: List[Dict]) -> List[Dict]:
        """Analyze multiple findings in single API call"""
        prompt = f"""Analyze these {len(findings)} secret findings. Return a JSON array with analysis for each.

Findings:
{json.dumps([self._finding_summary(f) for f in findings], indent=2)}

For each finding, provide:
{{
  "severity": "critical|high|medium|low",
  "confidence": 0.0-1.0,
  "reasoning": "explanation",
  "exposure_scope": "what this accesses",
  "blast_radius": "potential impact",
  "remediation_priority": "immediate|urgent|normal|low",
  "suggested_actions": ["action1", "action2", ...],
  "false_positive_likelihood": 0.0-1.0,
  "exploitation_difficulty": "trivial|easy|moderate|hard",
  "business_impact": "description"
}}

Return JSON array only (no markdown):"""

        response = self.client.messages.create(
            model=self.model,
            max_tokens=4000,
            temperature=0.0,
            messages=[{"role": "user", "content": prompt}]
        )
        
        return json.loads(response.content[0].text)
    
    def _build_analysis_prompt(self, finding: Dict) -> str:
        """Build detailed analysis prompt"""
        return f"""Analyze this secret finding for security risk assessment:

**Secret Details:**
- Type: {finding['secret_type']}
- Verified: {finding['verified']}
- Repository: {finding.get('repo_url', 'Unknown')}
- File Path: {finding['file_path']}
- Line Number: {finding['line_number']}
- Commit: {finding.get('commit_hash', 'Unknown')[:8]}
- Author: {finding.get('author', 'Unknown')}
- Commit Message: {finding.get('commit_message', 'N/A')[:100]}

**Code Context:**
```
{finding.get('code_context', 'No context available')}
```

Provide comprehensive security analysis in JSON format:
{{
  "severity": "critical|high|medium|low",
  "confidence": 0.0-1.0,
  "reasoning": "detailed explanation of severity assessment",
  "exposure_scope": "specific systems/data this credential can access",
  "blast_radius": "what could happen if exploited",
  "remediation_priority": "immediate|urgent|normal|low",
  "suggested_actions": [
    "specific action 1",
    "specific action 2",
    "specific action 3"
  ],
  "false_positive_likelihood": 0.0-1.0,
  "exploitation_difficulty": "trivial|easy|moderate|hard",
  "business_impact": "description of business consequences"
}}

**Analysis Guidelines:**
- Consider file location (config files, root, vendor code)
- Evaluate commit message context
- Assess if this is production code vs tests
- Consider verification status
- Evaluate exposure based on secret type

Respond ONLY with valid JSON (no markdown, no explanation):"""
    
    def _finding_summary(self, finding: Dict) -> Dict:
        """Create compact finding summary for batch processing"""
        return {
            'id': finding['id'],
            'type': finding['secret_type'],
            'verified': finding['verified'],
            'file': finding['file_path'],
            'commit_msg': finding.get('commit_message', '')[:50]
        }
    
    def _generate_cache_key(self, finding: Dict) -> str:
        """Generate cache key for finding"""
        key_data = f"{finding['secret_type']}:{finding['file_path']}:{finding.get('commit_hash', '')}"
        return hashlib.sha256(key_data.encode()).hexdigest()
    
    def _get_default_analysis(self) -> Dict:
        """Default analysis when AI fails"""
        return {
            'severity': 'medium',
            'confidence': 0.5,
            'reasoning': 'AI analysis unavailable',
            'exposure_scope': 'Unknown',
            'blast_radius': 'Unknown',
            'remediation_priority': 'normal',
            'suggested_actions': ['Manually review this finding'],
            'false_positive_likelihood': 0.5,
            'exploitation_difficulty': 'moderate',
            'business_impact': 'Unknown'
        }


class AIAnalysisCache:
    """Simple in-memory cache for AI analyses"""
    
    def __init__(self):
        self.cache = {}
    
    def get(self, key: str) -> Optional[Dict]:
        return self.cache.get(key)
    
    def set(self, key: str, value: Dict):
        self.cache[key] = value
    
    def clear(self):
        self.cache.clear()
```

### Week 6: Natural Language Query Agent

**Implementation:** See full project plan above for complete `ai/query_agent.py` implementation.

### Week 7: Similarity Detection & Clustering

**Implementation:** See full project plan above for complete `ai/similarity_detector.py` implementation.

### Week 8: Behavioral Anomaly Detection

**Implementation:** See full project plan above for complete `ai/behavior_analyzer.py` implementation.

---

## Phase 3: Graph Database & Analytics (Weeks 9-10)

### Week 9: Neo4j Integration

#### `graph/ingestion.py`

```python
from neo4j import GraphDatabase
from typing import List, Dict
import logging
from datetime import datetime

logger = logging.getLogger(__name__)

class GraphIngestionPipeline:
    """Ingest scan results into Neo4j"""
    
    def __init__(self, driver):
        self.driver = driver
    
    def ingest_scan_results(self, results: List[Dict], repo_info: Dict):
        """Bulk ingest with transaction management"""
        with self.driver.session() as session:
            session.execute_write(self._bulk_ingest, results, repo_info)
    
    def _bulk_ingest(self, tx, results: List[Dict], repo_info: Dict):
        """Efficient bulk insert"""
        # Create/update repository
        tx.run("""
            MERGE (r:Repository {name: $name})
            SET r.organization = $org,
                r.url = $url,
                r.visibility = $visibility,
                r.language = $language,
                r.size = $size,
                r.last_scanned = datetime(),
                r.updated_at = datetime($updated_at)
        """, 
            name=repo_info['repo_name'],
            org=repo_info.get('organization'),
            url=repo_info['repo_url'],
            visibility=repo_info.get('visibility', 'unknown'),
            language=repo_info.get('language'),
            size=repo_info.get('size', 0),
            updated_at=repo_info.get('updated_at', datetime.now().isoformat())
        )
        
        # Batch process findings
        for batch in self._batch_generator(results, 100):
            self._ingest_batch(tx, batch, repo_info['repo_name'])
    
    def _ingest_batch(self, tx, findings: List[Dict], repo_name: str):
        """Process a batch of findings"""
        tx.run("""
            UNWIND $findings as finding
            
            MATCH (r:Repository {name: $repo_name})
            
            MERGE (c:Commit {hash: finding.commit_hash})
            ON CREATE SET 
                c.timestamp = datetime(finding.commit_time),
                c.author = finding.author,
                c.message = finding.message,
                c.branch = finding.branch
            
            CREATE (s:SecretFinding {
                id: finding.id,
                secret_type: finding.secret_type,
                verified: finding.verified,
                file_path: finding.file_path,
                line_number: finding.line_number,
                first_detected: datetime(),
                status: 'open',
                code_context: finding.code_context
            })
            
            MERGE (r)-[:HAS_COMMIT]->(c)
            MERGE (c)-[:CONTAINS_SECRET]->(s)
            
            MERGE (d:Developer {email: finding.author})
            MERGE (d)-[:AUTHORED]->(c)
        """, findings=findings, repo_name=repo_name)
    
    def enrich_with_ai_analysis(self, secret_id: str, analysis: Dict):
        """Add AI analysis to graph"""
        with self.driver.session() as session:
            session.run("""
                MATCH (s:SecretFinding {id: $id})
                SET s.ai_severity = $severity,
                    s.ai_confidence = $confidence,
                    s.ai_reasoning = $reasoning,
                    s.ai_exposure_scope = $exposure_scope,
                    s.ai_blast_radius = $blast_radius,
                    s.ai_fp_likelihood = $fp_likelihood,
                    s.ai_exploitation_difficulty = $exploitation_difficulty,
                    s.ai_business_impact = $business_impact,
                    s.ai_analyzed_at = datetime()
                
                FOREACH (action IN $actions |
                    CREATE (a:RemediationAction {
                        description: action,
                        status: 'pending',
                        created_at: datetime()
                    })
                    MERGE (s)-[:REQUIRES_ACTION]->(a)
                )
            """, 
                id=secret_id,
                severity=analysis['severity'],
                confidence=analysis['confidence'],
                reasoning=analysis['reasoning'],
                exposure_scope=analysis['exposure_scope'],
                blast_radius=analysis['blast_radius'],
                fp_likelihood=analysis['false_positive_likelihood'],
                exploitation_difficulty=analysis['exploitation_difficulty'],
                business_impact=analysis['business_impact'],
                actions=analysis['suggested_actions']
            )
    
    def _batch_generator(self, items: List, batch_size: int):
        """Generate batches from list"""
        for i in range(0, len(items), batch_size):
            yield items[i:i+batch_size]
```

### Week 10: Advanced Analytics Queries

#### `graph/queries.py`

**Implementation:** See full project plan above for complete analytics query implementation.

---

## Phase 4: API & Dashboard (Weeks 11-13)

### Week 11: REST & GraphQL APIs

#### `api/rest_api.py`

**Implementation:** See full project plan above for complete FastAPI implementation.

### Week 12-13: Web Dashboard

**Tech Stack:**
- React 18 + TypeScript
- Vite for build tooling
- TanStack Query for data fetching
- Recharts for visualizations
- TailwindCSS for styling
- Socket.io for real-time updates

**Key Components:**
- Dashboard with stats cards
- Timeline charts
- Repository table with sorting/filtering
- Secret details view
- Natural language chat interface
- Developer behavior analysis view
- Real-time notifications

---

## Phase 5: Notifications & Reporting (Week 14)

### Notification Channels

#### `notifications/slack.py`

**Implementation:** See full project plan above for Slack notification implementation.

#### `notifications/email.py`

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from typing import List, Dict
import logging

logger = logging.getLogger(__name__)

class EmailNotifier:
    """Email notification service"""
    
    def __init__(self, smtp_config: Dict):
        self.smtp_host = smtp_config['host']
        self.smtp_port = smtp_config['port']
        self.smtp_user = smtp_config['username']
        self.smtp_pass = smtp_config['password']
        self.from_email = smtp_config['from_email']
    
    def send_executive_report(self, recipients: List[str], report: str, subject: str):
        """Send executive summary report"""
        msg = MIMEMultipart('alternative')
        msg['Subject'] = subject
        msg['From'] = self.from_email
        msg['To'] = ', '.join(recipients)
        
        # Plain text version
        text_part = MIMEText(report, 'plain')
        msg.attach(text_part)
        
        # HTML version (convert markdown to HTML)
        html_content = self._markdown_to_html(report)
        html_part = MIMEText(html_content, 'html')
        msg.attach(html_part)
        
        self._send_email(msg, recipients)
    
    def send_verified_secret_alert(self, recipient: str, secret: Dict):
        """Send alert for verified secret"""
        subject = f"🚨 Critical: Verified Secret Found in {secret['repo_name']}"
        
        body = f"""
A verified, active secret has been detected in your repository.

Repository: {secret['repo_name']}
Secret Type: {secret['secret_type']}
File: {secret['file_path']}
Severity: {secret['ai_severity']}

AI Analysis:
{secret['ai_reasoning']}

Suggested Actions:
""" + '\n'.join(f"- {action}" for action in secret['suggested_actions'])
        
        body += f"\n\nView Details: https://secretguard.example.com/secrets/{secret['id']}"
        
        msg = MIMEText(body)
        msg['Subject'] = subject
        msg['From'] = self.from_email
        msg['To'] = recipient
        
        self._send_email(msg, [recipient])
    
    def _send_email(self, msg: MIMEMultipart, recipients: List[str]):
        """Send email via SMTP"""
        try:
            with smtplib.SMTP(self.smtp_host, self.smtp_port) as server:
                server.starttls()
                server.login(self.smtp_user, self.smtp_pass)
                server.send_message(msg)
            
            logger.info(f"Email sent to {recipients}")
        except Exception as e:
            logger.error(f"Failed to send email: {e}")
    
    def _markdown_to_html(self, markdown: str) -> str:
        """Convert markdown to HTML (simple version)"""
        import markdown
        return markdown.markdown(markdown)
```

---

## Phase 6: Testing & Deployment (Weeks 15-16)

### Week 15: Comprehensive Testing

**Test Structure:**

```python
# tests/test_scanner.py
import pytest
from scanner.repo_enumerator import RepoEnumerator
from scanner.prioritizer import RepoPrioritizer

def test_repo_enumeration(github_token, test_org):
    """Test GitHub repo enumeration"""
    enumerator = RepoEnumerator(github_token, test_org)
    repos = enumerator.enumerate_org_repos()
    
    assert len(repos) > 0
    assert all('name' in r for r in repos)
    assert all('url' in r for r in repos)

def test_prioritization():
    """Test risk scoring algorithm"""
    repos = [
        {'name': 'test1', 'visibility': 'public', 'size': 50000, 
         'updated_at': datetime.now(), 'topics': ['aws', 'production']},
        {'name': 'test2', 'visibility': 'private', 'size': 1000,
         'updated_at': datetime.now() - timedelta(days=100), 'topics': []}
    ]
    
    prioritizer = RepoPrioritizer()
    prioritized = prioritizer.prioritize(repos)
    
    assert prioritized[0]['name'] == 'test1'  # Public with AWS topic should be higher

# tests/test_ai.py
def test_secret_analysis(mock_anthropic):
    """Test AI secret analysis"""
    analyzer = AISecretAnalyzer(api_key="test")
    
    finding = {
        'id': 'test123',
        'secret_type': 'AWS Access Key',
        'verified': True,
        'file_path': 'config/production.env',
        'line_number': 10
    }
    
    analysis = analyzer.analyze_secret(finding)
    
    assert 'severity' in analysis
    assert analysis['severity'] in ['critical', 'high', 'medium', 'low']
    assert 'reasoning' in analysis

# tests/performance/test_load.py
def test_concurrent_scans():
    """Test system under load"""
    # Simulate 10 concurrent scans
    pass

def test_large_repo_scan():
    """Test scanning large repositories"""
    # Test with repo > 1GB
    pass
```

### Week 16: Deployment

#### Production Docker Compose

```yaml
# docker-compose.prod.yml
version: '3.8'

services:
  neo4j:
    image: neo4j:5.15-enterprise
    environment:
      - NEO4J_AUTH=neo4j/${NEO4J_PASSWORD}
      - NEO4J_ACCEPT_LICENSE_AGREEMENT=yes
      - NEO4J_dbms_memory_heap_max__size=4G
      - NEO4J_dbms_memory_pagecache_size=2G
      - NEO4J_dbms_security_auth__enabled=true
    volumes:
      - neo4j_data:/data
      - neo4j_logs:/logs
    ports:
      - "7474:7474"
      - "7687:7687"
    networks:
      - secretguard
    deploy:
      resources:
        limits:
          memory: 8G
          cpus: '4'
    restart: unless-stopped
  
  postgres:
    image: postgres:15
    environment:
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - POSTGRES_DB=secretguard
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - secretguard
    restart: unless-stopped
  
  scanner:
    build:
      context: .
      dockerfile: Dockerfile.scanner
    environment:
      - GITHUB_TOKEN=${GITHUB_TOKEN}
      - ANTHROPIC_API_KEY=${ANTHROPIC_API_KEY}
      - NEO4J_URI=bolt://neo4j:7687
      - NEO4J_USER=neo4j
      - NEO4J_PASSWORD=${NEO4J_PASSWORD}
      - POSTGRES_URI=postgresql://postgres:${POSTGRES_PASSWORD}@postgres:5432/secretguard
    depends_on:
      - neo4j
      - postgres
    networks:
      - secretguard
    deploy:
      replicas: 3
    restart: unless-stopped
  
  api:
    build:
      context: .
      dockerfile: Dockerfile.api
    ports:
      - "8000:8000"
    environment:
      - NEO4J_URI=bolt://neo4j:7687
      - NEO4J_USER=neo4j
      - NEO4J_PASSWORD=${NEO4J_PASSWORD}
      - ANTHROPIC_API_KEY=${ANTHROPIC_API_KEY}
      - POSTGRES_URI=postgresql://postgres:${POSTGRES_PASSWORD}@postgres:5432/secretguard
    depends_on:
      - neo4j
      - postgres
    networks:
      - secretguard
    restart: unless-stopped
  
  dashboard:
    build:
      context: ./dashboard
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    environment:
      - API_URL=http://api:8000
    depends_on:
      - api
    networks:
      - secretguard
    restart: unless-stopped
  
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./ssl:/etc/nginx/ssl:ro
    depends_on:
      - api
      - dashboard
    networks:
      - secretguard
    restart: unless-stopped

networks:
  secretguard:
    driver: bridge

volumes:
  neo4j_data:
  neo4j_logs:
  postgres_data:
```

#### Kubernetes Deployment

```yaml
# k8s/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: secretguard-scanner
  namespace: secretguard
spec:
  replicas: 5
  selector:
    matchLabels:
      app: scanner
  template:
    metadata:
      labels:
        app: scanner
    spec:
      containers:
      - name: scanner
        image: secretguard/scanner:latest
        env:
        - name: GITHUB_TOKEN
          valueFrom:
            secretKeyRef:
              name: secretguard-secrets
              key: github-token
        - name: ANTHROPIC_API_KEY
          valueFrom:
            secretKeyRef:
              name: secretguard-secrets
              key: anthropic-key
        - name: NEO4J_URI
          value: bolt://neo4j-service:7687
        - name: NEO4J_PASSWORD
          valueFrom:
            secretKeyRef:
              name: secretguard-secrets
              key: neo4j-password
        resources:
          requests:
            memory: "2Gi"
            cpu: "1"
          limits:
            memory: "4Gi"
            cpu: "2"
---
apiVersion: v1
kind: Service
metadata:
  name: secretguard-api
  namespace: secretguard
spec:
  selector:
    app: api
  ports:
  - port: 8000
    targetPort: 8000
  type: LoadBalancer
```

---

## Resource Requirements

### Personnel

| Role | Time Commitment | Responsibilities |
|------|----------------|------------------|
| Lead Engineer | Full-time (100%) | Architecture, core development, AI integration |
| Backend Engineer | Part-time (50%, optional) | API development, database optimization |
| Frontend Engineer | Part-time (50%, optional) | Dashboard development |
| DevOps Engineer | Part-time (25%) | Deployment, CI/CD, monitoring |
| Security Reviewer | Part-time (10%) | Security review, validation |

### Infrastructure

**Development Environment:**
- Local development machines
- Development Neo4j instance (Docker)
- Test GitHub organization with sample repos
- Development API keys

**Production Environment:**

| Component | Specifications | Monthly Cost |
|-----------|---------------|--------------|
| Neo4j Server | 8GB RAM, 4 vCPUs, 100GB SSD | $200-300 |
| PostgreSQL | 4GB RAM, 2 vCPUs, 50GB SSD | $100-150 |
| Scanner Workers (3x) | 2GB RAM each | $150-200 |
| API Server | 4GB RAM, 2 vCPUs | $100-150 |
| Dashboard | 2GB RAM, 1 vCPU | $50-75 |
| Load Balancer | Standard | $20-30 |
| **Subtotal Infrastructure** | | **$620-905** |
| Anthropic API (Claude) | Variable usage | $200-500 |
| **Total Monthly** | | **$820-1,405** |

### API Usage Estimates

**Anthropic Claude API Costs:**
- Input: $3 per 1M tokens (Sonnet 4)
- Output: $15 per 1M tokens (Sonnet 4)

**Estimated Monthly Usage (1,000 repos, weekly scans):**
- ~10,000 secrets found per month
- AI analysis: 500 tokens in, 300 tokens out per secret
  - Input: (10,000 × 500) / 1M × $3 = $15
  - Output: (10,000 × 300) / 1M × $15 = $45
  - **Analysis subtotal: $60/month**
- Natural language queries: ~100/day
  - ~200 tokens in, 150 tokens out per query
  - Monthly: (100 × 30 × 200) / 1M × $3 + (100 × 30 × 150) / 1M × $15 = $86
- Reports: Daily executive summary
  - ~1,000 tokens in, 500 tokens out
  - Monthly: (30 × 1,000) / 1M × $3 + (30 × 500) / 1M × $15 = $0.32
- **Total AI API: ~$150-500/month** (depends heavily on usage patterns)

---

## Timeline & Milestones

### Gantt Chart Overview

```
Weeks 1-4:   [████████████] Foundation & Core Infrastructure
Weeks 5-8:   [████████████] AI Integration
Weeks 9-10:  [██████] Graph Database & Analytics
Weeks 11-13: [█████████] API & Dashboard
Week 14:     [███] Notifications & Reporting
Weeks 15-16: [██████] Testing & Deployment
```

### Major Milestones

| Week | Milestone | Success Criteria |
|------|-----------|------------------|
| 4 | Basic scanning operational | Can enumerate and scan repos, store in Neo4j |
| 8 | AI features operational | All AI components working and integrated |
| 10 | Full graph analytics | Neo4j fully populated with optimized queries |
| 13 | User interfaces complete | Dashboard and APIs functional |
| 14 | Alerting operational | All notification channels working |
| 16 | Production ready | Deployed, tested, documented |

---

## Risk Assessment & Mitigation

### Technical Risks

| Risk | Impact | Likelihood | Mitigation Strategy |
|------|--------|------------|---------------------|
| GitHub API rate limits | High | Medium | Implement caching, exponential backoff, use GraphQL, request rate limit increase |
| Neo4j performance at scale | High | Medium | Index optimization, query tuning, consider sharding for >10M nodes |
| AI API costs exceed budget | Medium | Medium | Implement aggressive caching, batch processing, set spending alerts |
| TruffleHog false positives | Medium | High | AI filtering layer, allow users to mark false positives, maintain feedback loop |
| Large repo scan timeouts | Medium | Medium | Incremental scanning, timeout handling, resume capability, parallel processing |
| Network connectivity issues | Medium | Low | Retry logic with exponential backoff, queue persistence, offline mode |
| Data model changes | Low | Medium | Versioned migrations, backward compatibility, schema evolution strategy |

### Security Risks

| Risk | Impact | Likelihood | Mitigation Strategy |
|------|--------|------------|---------------------|
| Exposure of found secrets | Critical | Low | Encrypt at rest (PGP), strict access control, audit logging, data retention policies |
| Unauthorized dashboard access | High | Medium | Strong authentication (SSO), MFA, role-based access control |
| AI prompt injection | Medium | Low | Input sanitization, query validation, safety checks, output filtering |
| Leaked service credentials | Critical | Low | Secret management system (Vault), auto-rotation, least privilege |
| Insider threats | High | Low | Access logging, separation of duties, regular audits |

### Operational Risks

| Risk | Impact | Likelihood | Mitigation Strategy |
|------|--------|------------|---------------------|
| Alert fatigue | High | High | AI-powered prioritization, smart grouping, configurable thresholds, summary digests |
| System downtime | Medium | Low | High availability setup, automated health checks, failover strategy |
| Data loss | High | Low | Regular backups (daily), point-in-time recovery, replication, disaster recovery plan |
| Maintenance burden | Medium | Medium | Comprehensive documentation, automation, monitoring, runbooks |
| Team turnover | Medium | Low | Documentation, knowledge transfer, modular architecture |

---

## Success Metrics

### Technical Performance Metrics

- **System Uptime:** 95%+ availability
- **Scan Performance:** < 24 hour complete scan cycle for all repos
- **API Response Time:** < 2 seconds (p95), < 500ms (p50)
- **Test Coverage:** 80%+ code coverage
- **False Positive Rate:** < 5% (with AI filtering)
- **Database Query Performance:** < 1 second for analytics queries

### Security Effectiveness Metrics

- **Detection Speed:** 100% of verified secrets alerted within 1 hour of discovery
- **Remediation Speed:** 90% of critical secrets remediated within 48 hours
- **Mean Time to Detection (MTTD):** < 24 hours from commit to detection
- **Mean Time to Remediation (MTTR):** < 7 days from detection to remediation
- **Coverage:** 100% of active repositories scanned weekly

### AI Quality Metrics

- **AI Severity Accuracy:** >85% agreement with human security expert review
- **Natural Language Query Success Rate:** >90% of queries return useful results
- **False Positive Prediction Accuracy:** >80% accuracy in identifying false positives
- **Report Usefulness Score:** >4/5 average rating from stakeholders
- **Analysis Consistency:** <10% variance in repeated analyses of same secret

### Business Impact Metrics

- **Secrets Found and Remediated:** Track total count and trend over time
- **Credential Exposure Reduction:** Measure decrease in active exposed credentials
- **Time Saved:** Calculate hours saved vs manual security reviews
- **Security Posture Improvement:** Reduction in security audit findings
- **Team Satisfaction:** >4/5 satisfaction score from security team
- **Executive Visibility:** Monthly reports delivered on time

---

## Documentation Requirements

### Technical Documentation

1. **Architecture Documentation**
   - System architecture diagram
   - Component interaction diagrams
   - Data flow diagrams
   - Technology stack documentation
   - Deployment architecture

2. **API Documentation**
   - OpenAPI/Swagger specification
   - GraphQL schema documentation
   - Authentication guide
   - Rate limiting policies
   - Example requests and responses

3. **Database Documentation**
   - Neo4j schema documentation
   - PostgreSQL schema documentation
   - Index strategy
   - Query optimization guide
   - Backup and restore procedures

4. **Deployment Guide**
   - Environment setup
   - Configuration management
   - Docker deployment
   - Kubernetes deployment
   - Scaling guidelines

5. **Operations Runbook**
   - Common issues and solutions
   - Troubleshooting guide
   - Performance tuning
   - Disaster recovery procedures
   - Maintenance tasks

### User Documentation

1. **User Guide**
   - Getting started
   - Dashboard navigation
   - Understanding risk scores
   - Interpreting AI analysis
   - Remediation workflows

2. **Query Guide**
   - Natural language query examples
   - Common use cases
   - Advanced query patterns
   - Cypher query reference

3. **Best Practices Guide**
   - Secret prevention strategies
   - Remediation best practices
   - Team workflows
   - Integration with existing tools

4. **FAQ**
   - Common questions
   - Troubleshooting tips
   - Feature explanations

### Developer Documentation

1. **Contributing Guide**
   - Code style guidelines
   - Git workflow
   - Pull request process
   - Code review checklist

2. **Development Setup**
   - Local environment setup
   - Running tests
   - Debugging guide
   - Development tools

3. **Testing Guide**
   - Testing philosophy
   - Writing unit tests
   - Integration testing
   - Performance testing

---

## Post-Launch Plan

### Weeks 17-18: Monitoring & Optimization

**Activities:**
- Set up comprehensive monitoring (Prometheus + Grafana)
  - System metrics (CPU, memory, disk)
  - Application metrics (scan duration, API latency)
  - Business metrics (secrets found, remediation rate)
- Tune performance based on real usage patterns
- Address any production issues
- Gather user feedback through surveys and interviews
- Create monitoring dashboards for different stakeholders

**Deliverables:**
- Monitoring dashboards operational
- Performance baseline established
- User feedback collected and prioritized
- Initial optimization implemented

### Weeks 19-20: Enhancement Iteration

**Activities:**
- Implement high-priority feature requests from user feedback
- Improve AI accuracy based on false positive/negative feedback
- Optimize costs (caching, batch processing improvements)
- Expand documentation based on common questions
- Conduct training sessions for users

**Deliverables:**
- Priority enhancements deployed
- Cost optimization report
- Training materials created
- Enhanced documentation

### Ongoing Maintenance Schedule

**Weekly Tasks:**
- Review alert quality and adjust thresholds
- Check system health and resource utilization
- Review and respond to user feedback
- Process false positive reports

**Monthly Tasks:**
- Generate and distribute executive reports
- Review and analyze key metrics
- Security audit of system
- Backup verification
- Dependency updates

**Quarterly Tasks:**
- Major feature releases
- Comprehensive security review
- Performance optimization sprint
- Technology stack updates
- User satisfaction survey

**Annual Tasks:**
- Architecture review and planning
- Technology refresh evaluation
- Budget review and forecasting
- Disaster recovery drill

---

## Optional Future Enhancements

### Phase 2 Features (Post-Launch)

1. **JIRA Integration**
   - Automatic ticket creation for critical secrets
   - Workflow integration
   - Status synchronization

2. **Remediation Automation**
   - Auto-rotate AWS credentials
   - Integrate with HashiCorp Vault
   - Automated PR creation for fixes

3. **Compliance Reporting**
   - SOX compliance dashboards
   - PCI-DSS reporting
   - Custom compliance frameworks

4. **Mobile App**
   - iOS and Android apps
   - Push notifications
   - Quick remediation actions

5. **Machine Learning Enhancements**
   - Local ML models for pattern detection (reduce API costs)
   - Anomaly detection improvements
   - Predictive analytics for risk assessment

6. **Pre-Commit Integration**
   - Git hooks for local secret scanning
   - IDE plugins (VSCode, IntelliJ)
   - Real-time developer feedback

7. **Credential Vault Integration**
   - HashiCorp Vault integration
   - AWS Secrets Manager
   - Azure Key Vault
   - Automatic secret rotation

8. **Multi-Platform Support**
   - GitLab integration
   - Bitbucket integration
   - Azure DevOps
   - Self-hosted Git servers

9. **Advanced Visualizations**
   - 3D graph visualization
   - Interactive timelines
   - Heatmaps
   - Network diagrams

10. **Enterprise Features**
    - Multi-tenancy
    - Custom branding
    - Advanced RBAC
    - Single Sign-On (SAML, OAuth)

---

## Getting Started

### Immediate Next Steps (Week 1, Day 1)

**1. Set up project repository**
```bash
# Create repository
git init secretguard
cd secretguard

# Create basic structure
mkdir -p {scanner,ai,graph,api,dashboard,notifications,config,tests,docs,scripts}

# Initialize Python environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Create requirements.txt
cat > requirements.txt << EOF
anthropic>=0.18.0
neo4j>=5.15.0
psycopg2-binary>=2.9.9
fastapi>=0.109.0
uvicorn>=0.27.0
pydantic>=2.5.0
pytest>=7.4.0
python-dotenv>=1.0.0
requests>=2.31.0
PyGithub>=2.1.1
EOF

pip install -r requirements.txt
```

**2. Configure credentials**
```bash
# Create .env file
cat > .env << EOF
# GitHub
GITHUB_TOKEN=your_github_token_here
GITHUB_ORG=your_org_name

# Anthropic
ANTHROPIC_API_KEY=your_anthropic_key_here

# Neo4j
NEO4J_URI=bolt://localhost:7687
NEO4J_USER=neo4j
NEO4J_PASSWORD=your_neo4j_password

# PostgreSQL
POSTGRES_URI=postgresql://postgres:your_password@localhost:5432/secretguard

# Notifications
SLACK_WEBHOOK_URL=your_slack_webhook
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASS=your_password
EOF

# Add .env to .gitignore
echo ".env" >> .gitignore
echo "venv/" >> .gitignore
echo "__pycache__/" >> .gitignore
echo "*.pyc" >> .gitignore
```

**3. Start databases locally**
```bash
# Create docker-compose.yml
cat > docker-compose.yml << EOF
version: '3.8'
services:
  neo4j:
    image: neo4j:5.15
    ports:
      - "7474:7474"
      - "7687:7687"
    environment:
      - NEO4J_AUTH=neo4j/your_password
    volumes:
      - neo4j_data:/data

  postgres:
    image: postgres:15
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_PASSWORD=your_password
      - POSTGRES_DB=secretguard
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  neo4j_data:
  postgres_data:
EOF

# Start databases
docker-compose up -d

# Verify they're running
docker-compose ps
```

**4. Initialize database schemas**
```bash
# Create setup script
cat > scripts/setup_db.py << 'EOF'
from neo4j import GraphDatabase
import psycopg2

# Neo4j setup
neo4j_driver = GraphDatabase.driver(
    "bolt://localhost:7687",
    auth=("neo4j", "your_password")
)

with neo4j_driver.session() as session:
    # Create constraints
    session.run("CREATE CONSTRAINT repo_name IF NOT EXISTS FOR (r:Repository) REQUIRE r.name IS UNIQUE")
    session.run("CREATE CONSTRAINT commit_hash IF NOT EXISTS FOR (c:Commit) REQUIRE c.hash IS UNIQUE")
    session.run("CREATE CONSTRAINT secret_id IF NOT EXISTS FOR (s:SecretFinding) REQUIRE s.id IS UNIQUE")
    print("✓ Neo4j constraints created")

# PostgreSQL setup
pg_conn = psycopg2.connect("postgresql://postgres:your_password@localhost:5432/secretguard")
with pg_conn.cursor() as cursor:
    cursor.execute(open('scripts/schema.sql').read())
    pg_conn.commit()
    print("✓ PostgreSQL schema created")

print("✓ Database initialization complete")
EOF

python scripts/setup_db.py
```

**5. Run first test scan**
```bash
# Create test script
cat > scanner/test_scan.py << 'EOF'
from scanner.repo_enumerator import RepoEnumerator
from scanner.trufflehog_wrapper import TruffleHogScanner

# Test enumeration
enumerator = RepoEnumerator(token="your_github_token")
repos = enumerator.enumerate_user_repos()
print(f"Found {len(repos)} repositories")

# Test scan on first repo
if repos:
    scanner = TruffleHogScanner()
    results = scanner.scan_repo_full(repos[0]['url'])
    print(f"Found {results['total_found']} secrets")
EOF

python scanner/test_scan.py
```

---

## Conclusion

This comprehensive project plan provides a complete roadmap for building the SecretGuard AI Platform. The 16-20 week timeline is realistic for a skilled engineer with your background in cybersecurity and AI integration.

**Key Strengths of This Plan:**
- Modular architecture allows parallel development
- AI integration provides unique value proposition
- Graph database enables powerful analytics
- Multiple user interfaces for different personas
- Comprehensive testing and deployment strategy
- Clear success metrics and risk mitigation

**Next Steps:**
1. Review and adjust timeline based on available resources
2. Set up development environment (Day 1 tasks above)
3. Begin Phase 1, Week 1 implementation
4. Establish regular check-ins to track progress

This platform could be a significant contribution to security operations at Goldman Sachs or a strong portfolio project demonstrating your expertise in cybersecurity, AI, and software engineering.

Good luck with the implementation! 🚀
