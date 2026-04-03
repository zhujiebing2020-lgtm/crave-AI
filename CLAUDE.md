  
  
  
## Document Structure Overview  
  
| Section | Content |  
|---------|---------|  
| Global Guidelines | Language, security |  
| Core Principles | Fundamental principles |  
| Project Scaffolding | Project scaffolding standards |  
| Cognitive Mode | Working methodology |  
| Tool Preferences | Tool usage preferences |  
| Code Quality | Code quality standards |  
| Git Workflow | Git workflow |  
| AI Collaboration | AI collaboration standards |  
| Document Version Management | Document version management (key section) |  
  
---  
  
# Chapter-by-Chapter Explanation  
  
## 1. Global Guidelines  
  
| Original | Translation/Analysis |  
|----------|-------------------|  
| **Conversation Language**: Always respond in Chinese (中文) | **Dialog Language**: Always respond in Chinese. All output, explanations, and questions must be in Chinese |  
| **Override**: The user may temporarily override any rule below with an explicit instruction in conversation | **Override**: The user may temporarily override any rule below with an explicit instruction in conversation |  
  
**Security Protocol — Absolute Compliance**:  
- **Never commit secrets**: Confirm `.env` is in `.gitignore` before every commit. Never output API keys, passwords, or tokens in conversation.  
  
---  
  
## 2. Core Principles  
  
| Original | Translation/Analysis |  
|----------|-------------------|  
| **Challenge Before Execute**: If the requirement seems off (wrong direction, wrong problem, or a more fundamental solution exists), raise it before acting — even when the instruction is clear | **Challenge Before Execute**: If the requirement seems off (wrong direction, wrong problem, or a more fundamental solution exists), raise it before acting — even when the instruction is clear |  
| **Suggest Shorter Paths**: When the goal is clear but the chosen path is suboptimal, proactively suggest a better approach and explain why | **Suggest Shorter Paths**: When the goal is clear but the chosen path is suboptimal, proactively suggest a better approach and explain why |  
| **Minimal Change**: Only touch what's necessary. Minimize code impact. Avoid introducing new bugs | **Minimal Change**: Only touch what's necessary. Minimize code impact. Avoid introducing new bugs |  
| **Root Cause, Not Patches**: Find the root cause; don't apply temporary patches. Maintain senior developer standards | **Root Cause, Not Patches**: Find the root cause; don't apply temporary patches. Maintain senior developer standards |  
  
**Interpretation**: This defines that AI should not just be an "obedient tool," but should possess **professional judgment** and **proactivity**.  
  
---  
  
## 3. Project Scaffolding  
  
Standard structure when initializing a new project:  
  
| Component | Description |  
|-----------|-------------|  
| **Root** | `.gitignore` (ignore rules), `.env.example` (environment variable example), `CLAUDE.md` (project-specific AI guidelines) |  
| **Docs** | `docs/architecture/` stores Architecture Decision Records (ADRs) |  
| **Source** | `src/` (organized by functional modules), `tests/` (mirrors src structure) |  
| **Safety Net** | Add global error handlers based on runtime |  
| **Toolchain** | Adapt linter, test framework, package manager based on project language |  
  
---  
  
## 4. Cognitive Mode  
  
| Original | Translation/Analysis |  
|----------|-------------------|  
| **One Topic Per Chat**: When conversation drifts off-topic, suggest `/clear` | **One Topic Per Chat**: When conversation drifts off-topic, suggest `/clear` |  
| **Plan Mode**: Enter Plan Mode when 3+ files are involved, architectural decisions are needed, or the approach is unclear | **Plan Mode**: Enter Plan Mode when 3+ files are involved, architectural decisions are needed, or the approach is unclear |  
| **LSP First**: Prefer LSP tools (Go to Definition, Find References) for code navigation; fall back to Grep/Glob only when LSP is unavailable | **LSP First**: Prefer LSP tools (Go to Definition, Find References) for code navigation; fall back to Grep/Glob only when LSP is unavailable |  
| **Self-Improvement**: After being corrected, record the lesson in auto memory. Review relevant memories at session start | **Self-Improvement**: After being corrected, record the lesson in auto memory. Review relevant memories at session start |  
  
---  
  
## 5. Tool Preferences  
  
| Original | Translation/Analysis |  
|----------|-------------------|  
| **File Operations**: Use Read/Edit/Write tools for single files; use Bash (cp, mv) for batch operations | **File Operations**: Use Read/Edit/Write tools for single files; use Bash (cp, mv) for batch operations |  
| **Search**: Prefer Agent tool (Explore subagent) for open-ended exploration; use Grep/Glob directly for targeted lookups | **Search**: Prefer Agent tool (Explore subagent) for open-ended exploration; use Grep/Glob directly for targeted lookups |  
| **Parallel Execution**: Use multiple parallel Agent calls when there are 2+ independent subtasks | **Parallel Execution**: Use multiple parallel Agent calls when there are 2+ independent subtasks |  
| **On Failure**: When a tool or command fails, report the error to the user and suggest alternatives — do not silently retry the same action | **On Failure**: When a tool or command fails, report the error to the user and suggest alternatives — do not silently retry the same action |  
  
---  
  
## 6. Code Quality  
  
| Original | Translation/Analysis |  
|----------|-------------------|  
| **Lint**: Configure linter + formatter during project init (ESLint/Prettier for JS/TS, Ruff for Python, etc.) | **Lint**: Configure linter + formatter during project init (ESLint/Prettier for JS/TS, Ruff for Python, etc.) |  
| **Type Safety**: Prefer TypeScript / Python type hints; avoid `any` / `@ts-ignore` | **Type Safety**: Prefer TypeScript / Python type hints; avoid `any` / `@ts-ignore` |  
| **Test Coverage**: Core logic must have unit tests | **Test Coverage**: Core logic must have unit tests |  
| **Elegance by Request**: Follow Minimal Change by default. Only pursue more elegant implementations when explicitly requested or when the current approach introduces obvious tech debt | **Elegance by Request**: Follow Minimal Change by default. Only pursue more elegant implementations when explicitly requested or when the current approach introduces obvious tech debt |  
  
---  
  
## 7. Git Workflow  
  
| Original | Translation/Analysis |  
|----------|-------------------|  
| **Commit Style**: Conventional Commits (`feat:`, `fix:`, `refactor:`) | **Commit Style**: Conventional Commits (`feat:`, `fix:`, `refactor:`) |  
| **Branch Naming**: `feature/`, `fix/`, `hotfix/` prefixes | **Branch Naming**: `feature/`, `fix/`, `hotfix/` prefixes |  
| **PR Size**: Keep under 400 lines when possible | **PR Size**: Keep under 400 lines when possible |  
| **Atomic Commits**: Each commit = one logical change | **Atomic Commits**: Each commit = one logical change |  
  
---  
  
## 8. AI Collaboration  
  
| Original | Translation/Analysis |  
|----------|-------------------|  
| **Ask First, Explain Why**: When implementation details are ambiguous, ask before implementing. After completion, explain *why* changes were made, not just *what* changed | **Ask First, Explain Why**: When implementation details are ambiguous, ask before implementing. After completion, explain *why* changes were made, not just *what* changed |  
| **Autonomous Bug Fixing**: On bug reports, locate and fix directly. But if the fix involves architectural choices or trade-offs, discuss before implementing | **Autonomous Bug Fixing**: On bug reports, locate and fix directly. But if the fix involves architectural choices or trade-offs, discuss before implementing |  
  
---  
  
## 9. Document Version Management (Key Section)  
  
This is the most detailed and standardized section of the entire document, defining **document types requiring version management** and **strict version control processes**.  
  
### 9.1 Document Types Requiring Version Management  
  
| Type | Example Filenames |  
|------|-----------------|  
| Requirements | `requirements.md`, `PRD.md`, etc. |  
| Planning | `roadmap.md`, `planning.md`, etc. |  
| Design | `design.md`, `architecture.md`, files under `specs/` directory |  
| Technical Proposals | `technical-proposal.md`, etc. |  
| Partnership Proposals | `partnership-proposal.md`, etc. |  
  
### 9.2 Version Annotation Format (Must be placed at end of document)  
  
```markdown  
---  
**Document Version**:  
  
**Created**: YYYY-MM-DD  
**Last Updated**: YYYY-MM-DD  
**Maintainer**: [Owner/Team Name]  
  
### Change Log  
  
| Version | Date | Major Changes | Reason |  
|---------|------|---------------|--------|  
| v1.0 | YYYY-MM-DD | Initial version | Project kickoff |  
```  
  
### 9.3 Version Update Workflow  
  
| Change Level | Version Change | Operation | Archival Requirement |  
|--------------|--------------|-----------|---------------------|  
| **Major** | v1.0 → v2.0 | Architecture adjustments, major requirement changes, technical direction shifts | Move old version to `docs/archive/[filename]-v1.0-YYYYMMDD.md` |  
| **Minor** | v1.0 → v1.1 | Feature additions/removals, module adjustments, content supplements | Move old version to `docs/archive/[filename]-v1.0-YYYYMMDD.md` |  
| **Patch** | v1.0 → v1.0.1 | Bug fixes, formatting adjustments, text improvements | **No archival** — only update "Last Updated" date |  
  
### 9.4 Archive Directory Structure  
  
```  
docs/  
├── archive/  # Archive directory  
│   ├── requirements-v1.0-20260301.md  
│   ├── requirements-v1.1-20260305.md  
│   └── design-v1.0-20260310.md  
├── requirements.md  # Current version  
└── design.md  # Current version  
```  
  
### 9.5 Archive File Naming Convention  
  
- **Format**: `[original-filename]-v[version]-[archive-date-YYYYMMDD].md`  
- **Example**: `requirements-v1.0-20260301.md`  
- **Note**: Archived file content remains unchanged; version information is reflected in filename  
  
### 9.6 AI Assistant Execution Rules  
  
| Scenario | Operation |  
|----------|-----------|  
| **Creating new document** | Automatically add version info block (v1.0) |  
| **Modifying document** | 1. Check if document type requires version management<br>2. Assess change level (Major/Minor/Patch)<br>3. If archival needed, copy current version to `docs/archive/` first<br>4. Update version number and changelog<br>5. **Inform user of version change** |  
| **Rolling back to old version** | Restore specified version from archive directory |  
  
---  
  
## Core Philosophy Summary  
  
| Dimension | Core Concept |  
|-----------|--------------|  
| **Professionalism** | Think like a senior developer, not just execute commands |  
| **Proactivity** | Identify problems, propose suggestions, pursue optimal solutions |  
| **Standardization** | Strict code quality, Git workflow, document version management |  
| **Security** | Never leak secrets; security by default |  
| **Collaboration** | Explain reasoning rather than just describing actions; maintain transparency |  
| **Traceability** | Document version management ensures decision history is trackable |  
  
This document is essentially a **"Professional Code of Conduct for AI Developers"**, ensuring AI assistants can collaborate with developers in a professional, reliable, and predictable manner in complex software projects.  
```  
  
