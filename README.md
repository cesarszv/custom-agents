# Custom Agents

Colección de agentes personalizados con un pipeline estructurado: se definen en español (staging), se traducen al inglés (production) y se despliegan a OpenCode (deploy).

## Estructura del Repositorio

```
source/                          ← Staging (español, source of truth)
resources/languages/en/source/   ← Production (traducciones en inglés)
.opencode/agents/                ← Deploy (archivos finales para OpenCode)
.agents/skills/                  ← Skills de gestión del pipeline
```

## Estándar de Archivos por Agente

Cada agente sigue la separación de responsabilidades:

| Archivo | Responsabilidad |
|---|---|
| `IDENTITY.md` | Propósito: qué hace, para quién, en qué dominio opera |
| `SOUL.md` | Constitución: personalidad, tono, valores, comportamiento |
| `AGENTS.md` | Configuración: reglas operativas, expertise, convenciones |
| `README.md` | Documentación para humanos (no es parte del estándar de agentes) |

## Agentes

| Agente | Dominio |
|---|---|
| **Diana** | Productividad, gestión del tiempo, metodologías de organización |
| **JJ** | Arquitectura de software, CS, IA, desarrollo full-stack |
| **Marty McBot** | Deep research histórico, soluciones del pasado |
| **Obsi** | Gestión del Conocimiento Personal (PKM), Obsidian.md |
| **Yupi Dupi** | Orquestador principal *(en diseño)* |
| **Yurnal** | Psicología académica |

## Skills de Gestión

| Skill | Función |
|---|---|
| `agent-scaffold` | Crea un agente nuevo en las 3 capas |
| `agent-sync` | Sincroniza staging (ES) → production (EN) |
| `agent-to-opencode` | Genera archivos de deploy desde las fuentes EN |
| `agent-audit` | Verifica consistencia entre capas |

## Workflow

1. **Crear**: `agent-scaffold` genera la estructura del agente
2. **Editar**: modificar archivos en `source/<Agente>/`
3. **Sincronizar**: `agent-sync` actualiza las traducciones EN
4. **Desplegar**: `agent-to-opencode` genera los archivos `.opencode`
5. **Verificar**: `agent-audit` valida consistencia
