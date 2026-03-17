sequenceDiagram
  autonumber

  participant U as User / Client App (SDK, Web App)
  participant P as Foundry Project Endpoint<br/>https://<account>.services.ai.azure.com/api/projects/<project>
  participant O as Foundry Agent Service Runtime (Orchestrator)
  participant M as Foundry Models inference endpoint (deployments)
  participant T as Tool Boundary (registered tools only)

  participant COS as Azure Cosmos DB for NoSQL<br/>(threads/state storage)
  participant STG as Azure Storage Account<br/>(file storage)
  participant AIS as Azure AI Search<br/>(retrieval/grounding)

  participant MCP as MCP Server Endpoint<br/>(hosted or customer-hosted)
  participant APIC as Azure API Center (optional)
  participant INTAPI as Internal / Private API (LOB)

  U->>P: HTTPS + Entra token<br/>Create/continue agent run
  P->>O: Start run / resume thread

  O->>COS: Read/write thread state<br/>(conversation context)
  COS-->>O: Thread context

  O->>M: LLM inference request<br/>(prompt + context)
  M-->>O: Model response<br/>(may include tool intent)

  alt Needs Azure AI Search tool
    O->>T: Invoke tool (AI Search)
    T->>AIS: Query index via project connection / RBAC
    AIS-->>T: Retrieved passages + citations
    T-->>O: Tool result
  else Needs file access (Storage)
    O->>T: Invoke tool (Files)
    T->>STG: Read/write documents
    STG-->>T: File content / pointer
    T-->>O: Tool result
  else Needs MCP tool
    O->>T: Invoke MCP tool<br/>(approved/authorized)
    opt MCP catalog metadata exists
      MCP-->>APIC: Server registered (metadata)
    end
    T->>MCP: HTTPS call to MCP server endpoint
    MCP->>INTAPI: Validate request + call internal API
    INTAPI-->>MCP: Result payload
    MCP-->>T: Tool result
    T-->>O: Tool result
  end

  O->>M: Follow-up inference<br/>(tool results + updated context)
  M-->>O: Final answer
  O-->>P: Response payload
  P-->>U: Final response
