# 🤖 Agentic MCP Orchestrator (OpenCode Edition)

> Un Agente Autónomo que construye su propio ecosistema de herramientas. No usa herramientas pre-configuradas — las descubre, instala y orchestra bajo demanda.

---

## Problema

Los agentes LLM actuales dependen de herramientas pre-configuradas. Si la herramienta no existe, el agente fracasa. Este proyecto cambia el paradigma:

```
Usuario: " necesito una API REST que conecte a mi PostgreSQL"
         │
         ▼
   Agente Autónomo
   ┌──────────────────────────────────────┐
   │ 1. Razono qué necesito: DB + API    │
   │ 2. Descubro: @modelcontextprotocol/   │
   │             postgres-server         │
   │ 3. Provisiono: npm install ...        │
   │ 4. Configuro: DATABASE_URL=...       │
   │ 5. Ejecuto: creo la API               │
   │ 6. Reflecciono: funcionó?            │
   │ 7. Persisto: "Prompt → Tools → OK"     │
   └──────────────────────────────────────┘
```

## Visión

Un agente que:
- **Razonas** sobre qué herramientas necesita para cada tarea
- **Descubres** herramientas en el ecosistema MCP
- **Provisionas** (instalas/configuras) dinámicamente
- **Ejecutas** pipelines complejos
- **Aprendes** de cada éxito/fallo

---

## Arquitectura

```
┌─────────────────────────────────────────────────────────┐
│                    OpenCode Runtime                      │
│  ┌─────────────────────────────────────────────────┐   │
│  │           Core Loop (Chain-of-Thought)            │   │
│  │  Ingesta → Planificación → Discovery →        │   │
│  │  Provisionamiento → Ejecución →              │   │
│  │  Reflexión → Persistencia                    │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                          │
         ┌────────────────┼────────────────┐
         ▼                ▼                ▼
   ┌───────────┐   ┌───────────┐   ┌───────────┐
   │  MCP     │   │ Vector   │   │  Skill   │
   │ Registry │   │   DB    │   │  Store   │
   │ (tools)  │   │(pgvector)│   │ (code)   │
   └───────────┘   └───────────┘   └───────────┘
                          │
                   ┌──────┴──────┐
                   ▼             ▼
            ┌──────────┐  ┌──────────┐
            │ Agent    │  │ Supabase │
            │ Memory  │  │   Pool   │
            └──────────┘  └──────────┘
```

---

## Componentes

### 1. mcp_registry
Catálogo de servidores MCP disponibles con metadata:

| Campo | Descripción |
|-------|-------------|
| `name` | Nombre del package |
| `capabilities` | Qué puede hacer (db, api, filesystem...) |
| `install_cmd` | Comando de instalación |
| `config_schema` | Variables requeridas |
| `rank` | Score basdo en uso/éxito |

### 2. agent_memory
Historial de ejecuciones:

| Campo | Descripción |
|-------|-------------|
| `prompt` | Input original |
| `tools_used` | MCPs instalados |
| `result` | éxito/error |
| `duration` | Tiempo de ejecución |
| `tokens_spent` | Costo en tokens |

### 3. skill_store
Código generado por el agente que se vuelve permanente:

| Campo | Descripción |
|-------|-------------|
| `name` | Nombre del skill |
| `code` | Código (Python/JS) |
| `trigger` | Cuándo ejecutarlo |
| `success_rate` | % de veces que funcionó |

---

## Flujo del Agente (Core Loop)

```python
async def agent_loop(user_prompt: str):
    # 1. Ingesta
    goal = parse(user_prompt)

    # 2. Planificación
    subtasks = decompose(goal)

    # 3. Discovery
    for task in subtasks:
        tools = search_mcp_registry(task, vector_db)
        best_tool = rank(tools).first

    # 4. Provisionamiento
    if not installed(best_tool):
        await provision(best_tool.install_cmd)
        await configure(best_tool.config)

    # 5. Ejecución
    result = await execute(best_tool, task)

    # 6. Reflexión
    if result.success:
        await index_memory(goal, tools, result)
    else:
        await retry_with_different_tool(task)
```

---

## Stack

| Componente | Tecnología |
|------------|-------------|
| Runtime | OpenCode |
| LLMs | Claude 3.5 Sonnet, GPT-4o, Gemini 1.5 Pro |
| Protocolo | Model Context Protocol (MCP) |
| Vector DB | Supabase (pgvector) |
| Orquestación | Plan-and-Execute |

---

## Roadmap

### Phase 1: Core Agent (MVP)
- [ ] Core loop básico en OpenCode
- [ ] tool-agnostic abstraction layer
- [ ] MCP Registry con top-servers pre-cargados
- [ ] Feedback loop básico (éxito/error)

### Phase 2: Discovery Engine
- [ ] Búsqueda semántica con embeddings
- [ ] Ranker basado en historial
- [ ] Tool comparison automático

### Phase 3: Auto-Provisioning
- [ ] Ciclo de autoinstalación npm
- [ ] Configuración automática de env vars
- [ ] Docker/Python provisioners

### Phase 4: Learning
- [ ] Agent memory indexing
- [ ] Skill store con código generado
- [ ] Success rate tracking

---

## Comparación

| Característica | Tool-Finder clásico | Agentic Orchestrator |
|----------------|-------------------|-------------------|
| Herramientas | Pre-configuradas | Bajo demanda |
| Razonamiento | None | Chain-of-Thought |
| Instalación | Manual | Automática |
| Aprendizaje | No | Sí |

---

## Instalación

```bash
# Por definir — aún en diseño
```

---

## Contributing

Este proyecto evoluciona rápidamente. Para contribuir:

1. Fork del repo
2. Define un nuevo capability en `mcp_registry`
3. Mejora el ranking algorithm
4. Añade tests en `core_loop.test.ts`

---

## Licencia

MIT