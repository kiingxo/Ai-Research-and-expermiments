# 4. Frameworks & Tools

Production frameworks and tools for deploying and running LLMs.

## Contents

- **LangGraph** - Agent framework for building AI applications
  - my note on LangGraph.txt
  - my note on Langraph 2.txt

- **Ollama** - Running LLMs locally
  - Llama3_(8B)_Ollama.ipynb - Local inference example

- *(More frameworks coming)*

## Frameworks

### LangGraph
**Purpose**: Build stateful, multi-actor applications with LLMs

**Key Features**:
- Agent orchestration
- Tool/API integration
- Memory management
- Streaming support

**Use Cases**:
- Multi-step agents
- Conversational applications
- Complex workflows
- Chain-of-thought reasoning

**Resources**:
- [LangGraph Documentation](https://langchain-ai.github.io/langgraph/)
- Notebooks in this folder

### Ollama
**Purpose**: Run LLMs locally without cloud dependencies

**Key Features**:
- Easy installation
- Multiple model support (Llama, Mistral, etc.)
- GPU optimization
- Fast inference

**Use Cases**:
- Local development
- Privacy-sensitive applications
- Offline deployment
- Experimentation

**Resources**:
- [Ollama Official Site](https://ollama.ai/)
- Example notebook: Llama3_(8B)_Ollama.ipynb

### Other Important Frameworks

#### LangChain
- LLM application development
- Chain composition
- Memory and retrieval
- Integration ecosystem

#### FastAPI + Transformers
- Production APIs
- High throughput
- Customizable
- Containerizable

#### vLLM
- High-throughput inference
- Continuous batching
- GPU optimization
- Drop-in replacement for transformers

#### Ray LLM
- Distributed serving
- Multiple models
- Scaling
- Production-grade

## Comparison Table

| Framework | Purpose | Local | Cloud | Complexity |
|-----------|---------|-------|-------|-----------|
| Ollama | Local inference | ✓ | ✗ | Low |
| LangGraph | Agent building | ✓ | ✓ | Medium |
| FastAPI | API serving | ✓ | ✓ | Medium |
| vLLM | Inference optimization | ✓ | ✓ | High |
| Ray LLM | Distributed serving | ✗ | ✓ | High |

## Quick Start

### Running Ollama
```bash
# Install: https://ollama.ai/
ollama pull llama2
ollama run llama2
```

### Using LangGraph
```python
from langgraph.graph import StateGraph

graph = StateGraph(AgentState)
graph.add_node("agent", agent)
graph.add_edge("agent", "end")
```

## Deployment Guide

1. **Development**: Use Ollama locally
2. **Testing**: Deploy with FastAPI
3. **Production**: Scale with vLLM or Ray
4. **Agents**: Use LangGraph for complex logic

## Next Steps

→ See **projects/** for real-world examples
→ Check **experiments/** for research implementations
