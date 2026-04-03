# Claude Code Architecture Diagrams

Interactive Mermaid.js visualization of Claude Code's 512K-line codebase.

> ⚠️ **Note**: GitHub README shows simplified overview diagrams only. For the **complete interactive visualization** with 81 Detail Panels and full architecture diagrams, please run the HTML file locally (see [Usage](#usage) below).

## 8 Systems Overview (Simplified)

```mermaid
flowchart TB
    subgraph CORE["1. CORE ENGINE"]
        MAIN["main.tsx"]
        QUERY["query/"]
        STATE["state/"]
    end

    subgraph UI["2. UI/RENDERING"]
        INK["ink/"]
        SCREENS["screens/"]
        COMPONENTS["components/"]
    end

    subgraph TOOLS["3. TOOLS (43)"]
        FILE_TOOLS["File Tools"]
        EXEC_TOOLS["Exec Tools"]
        AGENT_TOOLS["Agent Tools"]
    end

    subgraph COMMANDS["4. COMMANDS (100+)"]
        SESSION_CMD["Session"]
        CONFIG_CMD["Config"]
    end

    subgraph SERVICES["5. SERVICES"]
        API["Claude API"]
        MCP["MCP Protocol"]
        LSP["LSP Server"]
    end

    subgraph BRIDGE["6. BRIDGE/REMOTE"]
        BRIDGE_CORE["bridge/"]
        REMOTE["remote/"]
    end

    subgraph EXTENSIONS["7. EXTENSIONS"]
        SKILLS["skills/"]
        TASKS["tasks/"]
    end

    subgraph INFRA["8. INFRASTRUCTURE"]
        UTILS["utils/"]
        TYPES["types/"]
    end

    CORE --> UI --> TOOLS --> SERVICES --> BRIDGE
    EXTENSIONS --> CORE
    INFRA --> CORE
```

## Query Loop Flow

```mermaid
flowchart LR
    INPUT["User Input"] --> PROCESS["processUserInput()"]
    PROCESS --> API["Claude API"]
    API --> STREAM["Streaming Response"]
    STREAM --> TOOL{"Tool Use?"}
    TOOL -->|Yes| EXEC["Execute Tool"]
    EXEC --> API
    TOOL -->|No| RENDER["Render Output"]
    RENDER --> INPUT
```

## Files

| File | Description |
|------|-------------|
| [architecture-overview.html](architecture-overview.html) | Complete interactive visualization (100% coverage) |
| [COVERAGE-EVALUATION.md](COVERAGE-EVALUATION.md) | 127-item coverage tracking |

## Usage

```bash
# Start local server
npx serve .

# Open in browser
open http://localhost:3000/architecture-overview.html
```

## Coverage

| System | Items | Coverage |
|--------|-------|----------|
| Startup Flow | 12 | 100% |
| Query Loop | 10 | 100% |
| UI/Rendering | 11 | 100% |
| Tools System | 21 | 100% |
| Commands | 12 | 100% |
| Services | 18 | 100% |
| Bridge/Remote | 14 | 100% |
| Extensions | 10 | 100% |
| Infrastructure | 12 | 100% |
| **Total** | **127** | **100%** |

---
