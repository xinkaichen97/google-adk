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
uvx --from google-adk adk create --type=config day2-agent
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
adk create day3-agent
```

It creates an `agent.py` instead of a YAML file.

Update `agent.py` to use Google search and Gemini 3, then run locally:
```
curl 'https://raw.githubusercontent.com/GoogleCloudPlatform/devrel-demos/refs/heads/main/ai-ml/agent-labs/gemini-3-pro-agent-demo/my_agent/agent.py' > day3-agent/agent.py
adk web
```

## Day 4: Source-Based Deployment

Create a new project with Agent Starter Pack:
```
uvx agent-starter-pack create day4-agent -a adk_base -d agent_engine
cd day4-agent
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

## Day 6: ADK ready in Gemini CLI

Create a deep search agent:
```
uvx agent-starter-pack create day6-deep-search-agent --adk
cd day6-deep-search-agent
make install
```

Set up Gemini CLI:
```
pip install pydantic-ai
gemini extensions install https://github.com/derailed-dash/adk-docs-ext
gemini
```

Note: `gemini` needs to be installed, like `brew install gemini` for Mac.

## Day 7: LLMs Can Execute Code

Clone the repository and cd into the project directory:
```
git clone https://github.com/google/adk-samples.git
cd adk-samples/python/agents/retail-ai-location-strategy
```

Create a .env file in the app folder with your API keys:
```
cp .env.example .env
```
Update `GOOGLE_API_KEY` and `MAPS_API_KEY` (with Places API enabled).

Install & Run:
```
make install && make dev
```

The agent is now running at http://localhost:8501.

The sub-agent `gap_analysis_agent` calls code_executor=BuiltInCodeExecutor() to execute code.

