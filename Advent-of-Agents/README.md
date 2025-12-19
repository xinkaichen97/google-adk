# Advent of Agents

### 25 days of Agents in Google

https://adventofagents.com/

## Day 1: Launch Initiative

[Google ADK](https://google.github.io/adk-docs/): The Agent Development Kit

[The Agent Starter Pack](https://github.com/GoogleCloudPlatform/agent-starter-pack): End-to-end production-ready templates

## Day 2: Hello World with YAML

Get API keys in [Google AI Studio](https://aistudio.google.com/api-keys) 

Create and define the agent in the YAML file (): 
```
uvx --from google-adk adk create --type=config my_agent
```
It creates a `root_agent.yaml` because of `--type=config`.

Now to run it:
```
uvx --from google-adk adk web my_agent/
```
## Day 3: Gemini 3 + ADK

Option 1: One liner with Agent Starter Pack (uvx doesn't store the venv):
```
uvx agent-starter-pack create -y --api-key YOUR_GEMINI_API_KEY
```

Option 2: Create a venv using uv and then create an agent:
```
uv init
uv add google-adk
uv add google-genai
export GOOGLE_API_KEY="YOUR_API_KEY"
source .venv/bin/activate
adk create my_agent
```

It creates an `agent.py` instead of a YAML file.

Update `agent.py` and then run locally:
```
curl 'https://raw.githubusercontent.com/GoogleCloudPlatform/devrel-demos/refs/heads/main/ai-ml/agent-labs/gemini-3-pro-agent-demo/my_agent/agent.py' > my_agent/agent.py
adk web
```

## Day 4: Source-Based Deployment

Create new project with Agent Starter Pack:
```
uvx agent-starter-pack create my-agent -a adk_base -d agent_engine
cd my-agent
make deploy
```

Or to enhance existing ADK agents so that we can deploy:
```
uvx agent-starter-pack enhance -d agent_engine
```

To successfully deploy the agent, make sure to 
- Set up GCP credentials (account, project)
- Turn on both **Vertex AI API** and **Cloud Resource Manager API** in [APIs & Services](https://console.cloud.google.com/apis/)

## Day 5: Production Observability

Observe the deployed agent in [Agent Engines](https://console.cloud.google.com/vertex-ai/agents/agent-engines)

[Documentation](https://googlecloudplatform.github.io/agent-starter-pack/guide/observability.html) on production observability


