# Newo Agent Builder

Create, configure, test and launch AI receptionists and customer-service agents on the Newo platform from a conversation with Claude. The plugin pairs the Newo Customer MCP server with ten skills and three commands that tell Claude how to work with your Newo businesses safely: which tools to call, in what order, what to confirm with you first, and how to verify the result.

## What it does

- **Create an agent.** Give Claude your website or Google Maps link. Newo researches the business, creates it with an AI agent and a phone number, and Claude reports the agent number and portal link when provisioning finishes.
- **Configure.** Set business and persona attributes, languages, greetings, hours, transfers and reports, and run a health checkup of an existing agent.
- **Knowledge base.** Read, search, add and replace knowledge base topics and check which facts the agent retrieves.
- **Integrations and telephony.** Manage connectors, webhooks, voice and speech settings, SIP, call transfers and after-hours rollout.
- **Test and review.** Chat with the agent in the sandbox, review recent conversations, sessions and logs, and propose improvements you can verify.
- **Develop.** Write and review agent code and reusable Python WASM skills, and connect an external MCP server to an agent.
- **Roll out.** Plan acceptance criteria, rollout steps and draft support requests.

Commands: `/newo-agent-builder:build-agent`, `/newo-agent-builder:agent-checkup` and `/newo-agent-builder:review-conversations`. Skills load on their own when your request matches them.

## Requirements

You need a Newo account with access to at least one business, or permission to create one. Sign up or ask your Newo administrator at [newo.ai](https://newo.ai).

## Install and sign in

In Claude Code, install the plugin from this repository:

```
/plugin install newo-agent-builder --marketplace newo-ai/newo-claude-plugin
```

On older versions of Claude Code, add the marketplace first with `/plugin marketplace add newo-ai/newo-claude-plugin`, then run `/plugin install newo-agent-builder@newo`.

Then run `/mcp`, select the `newo` server and choose to authenticate. Your browser opens the Newo sign-in page. Claude Code uses a public OAuth client with PKCE and the scopes `openid offline_access`, and receives the result on `http://localhost:8765/callback`, so port 8765 must be free during sign-in. No password, API key or client secret is stored in the plugin.

In claude.ai and Cowork, add the plugin, then connect the Newo connector from the plugin's Connectors tab and sign in to Newo.

## Data and network access

The plugin contains only Markdown and JSON instructions. It runs no scripts or hooks on your computer and stores no data itself.

Every operation goes to one place: the Newo Customer MCP server at `https://api.newo.ai/api/v1/customer-mcp`, using your own Newo sign-in. Claude sends the business details you work on, such as website or Google Maps links for research, agent settings, knowledge base topics, connector settings and sandbox test messages. For reviews, Claude reads conversations, sessions and logs that your account is allowed to see. Newo's servers fetch the links you provide; Claude does not send data to any other service. Data that your account marks as protected health information stays restricted, and the plugin does not try to work around that restriction.

Newo handles this data under its [Privacy Policy](https://newo.ai/privacy-policy) and [Terms of Service](https://newo.ai/terms-of-service).

## Actions with cost or live impact

- Creating a business in standard mode purchases a phone number. Claude confirms the source link with you before it creates one.
- Starting a phone or SMS connector for the first time may purchase a number.
- Agent events and subscriptions can place real calls or send SMS and email. Claude asks for your authorization before real calls, messages or changes to a live line.

## Support

Email support@newo.ai or visit the [Newo help center](https://help.newo.ai/en/collections/17890660-support).

## License

MIT. See [LICENSE](LICENSE).
