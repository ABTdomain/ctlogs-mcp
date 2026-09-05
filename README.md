# CTlogs.io MCP server

Certificate Transparency, inside the conversation you are already having.

[CTlogs.io](https://ctlogs.io) runs a hosted [Model Context Protocol](https://modelcontextprotocol.io) server. Connect it to Claude, Cursor, or any client that speaks MCP, and your assistant can query the certificate index itself: which certificates have been issued for a hostname, by which certificate authority, and when they expire; or which certificate sits behind a fingerprint. You ask; it looks it up; you work with what comes back.

```
https://mcp.ctlogs.io/mcp
```

It is the same index and the same account you use on [ctlogs.io](https://ctlogs.io). What changes is who does the typing.

## Connect

You need a CTlogs account with an active plan. Plans and allowances are on the [pricing page](https://ctlogs.io/pricing).

Every client wants the same two things: the server address above, added as a remote or HTTP connector, and a sign-in. The client opens CTlogs in your browser, you sign in and approve the connection once. There is no key to copy and nothing to keep in a configuration file.

### Claude Code

```bash
claude mcp add --transport http ctlogs https://mcp.ctlogs.io/mcp
```

Then run `/mcp` inside Claude Code to complete the sign-in.

### Claude (web and desktop)

Settings, then Connectors, then *Add custom connector*. Name it CTlogs, paste the server address, and follow the sign-in prompt.

### Cursor

Add the server to your MCP settings (`.cursor/mcp.json` in a project, or the global file):

```json
{
  "mcpServers": {
    "ctlogs": {
      "url": "https://mcp.ctlogs.io/mcp"
    }
  }
}
```

Cursor offers the sign-in when it first connects to the server.

### Other clients

Any client that supports MCP over Streamable HTTP with OAuth sign-in works the same way.

## What your assistant can do

| Tool | The question it answers |
|---|---|
| `lookup_certificates` | The certificate history of one hostname, or the certificate behind a fingerprint |
| `index_status` | How large and how fresh the index is |
| `account_quota` | How much of your allowance is left |

Listing the subdomains of a domain and searching hostnames for a keyword are [DomainKits](https://domainkits.com/tools/subdomains) tools, from the same team; this server answers one question, which certificates exist for a name.

Every tool is read-only. Nothing the assistant can call changes anything.

The tools describe their own parameters to the client, so your assistant already knows how to call them. Current allowances and limits are on the [pricing page](https://ctlogs.io/pricing) and in the [API documentation](https://ctlogs.io/docs); they are not repeated here because they will change as the service settles in.

## Things to ask

- "Which certificates have been issued for api.example.com, from which certificate authority, and when does the latest one expire?"
- "Has anyone other than our usual certificate authority issued for www.example.com?"
- "Look up the certificate with this fingerprint, and tell me which names it covers."
- "How much of my allowance is left?"

## Good to know

- **One account, every client.** A laptop, an editor and a server can all be connected at once. They act as the same account, and usage is counted once.
- **Made for asking, not exporting.** Results are sized for a conversation. For bulk work, use the [API](https://ctlogs.io/docs) directly.
- **Public data, for security work.** Everything in the index comes from public Certificate Transparency logs: hostnames and certificate metadata such as the issuing certificate authority, dates and fingerprints. The service does not support looking up personal information; queries take a domain name, a hostname, a fingerprint or a word inside a hostname. It is built for security, brand protection and infrastructure work.
- **What the data means.** The index is built from public Certificate Transparency logs. It tells you which names have had certificates issued, from which certificate authority and when; it does not tell you whether a host is live or what it serves. Read [what Certificate Transparency actually tells you](https://ctlogs.io/blog/what-certificate-transparency-actually-tells-you) before drawing conclusions.

## Who makes this

CTlogs.io is built on the technology behind [ABTdomain.com](https://abtdomain.com), the domain intelligence platform, and shares its data and tooling with [Domainkits.com](https://domainkits.com), which covers domain search and newly registered domains. Certificate Transparency is one lens on the same picture: names appear in the domain registries, in DNS, and in the certificate logs, and the three sites look at the same names from those three sides.

Open source tools and datasets from the same team are on [github.com/ABTdomain](https://github.com/ABTdomain).

## Support

Questions and problems: [info@lyalpha-gmbh.com](mailto:info@lyalpha-gmbh.com), or open a ticket from the member area.

CTlogs.io is operated by Lyalpha GmbH, Düsseldorf, Germany. [Terms](https://ctlogs.io/terms) · [Privacy](https://ctlogs.io/privacy) · [Imprint](https://ctlogs.io/imprint)
