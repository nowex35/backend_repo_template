# backend_repo_template
This is nowex35's repo template for backend

### How to additional set up
1. serena mcp
  - コンテキスト整理用
  ```claude mcp add serena -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server --context ide-assistant --project $(pwd)```
1. chrome dev tools mcp
  - chrome dev toolsをAI-Agentが使えるようになるmcp
  ```
claude mcp add chrome-devtools npx chrome-devtools-mcp@latest
```