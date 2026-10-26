# Redeployment and Recovery Notes

**Purpose:** Keep Better Together Labs' operational knowledge version-controlled without publishing passwords, tokens, private client data, or machine-specific secrets.

## Sources of truth

- [Brand brief](../brand/BRAND-BRIEF.md)
- [CEO AGENTS.md](../agents/ceo/AGENTS.md)
- [Initial operating boundaries](../governance/OPERATING-BOUNDARIES.md)
- [Branding explorations](../marketing/branding/README.md) — protected; no changes without explicit founder authorization.

## Paperclip runtime — current architectural baseline

- Paperclip is deployed in **Docker Desktop on a Windows 11 desktop**, using the Linux container backend.
- The application is published on port **3100**, with a separate PostgreSQL container and persistent Docker volumes.
- The public-facing URL is **https://corpo.maynardfolks.com**, behind the existing Nginx Proxy Manager reverse proxy.
- Authentication is enabled. Treat the direct application port as restricted to trusted network paths, not a public bypass.
- Codex and Claude use existing subscription connections; **no paid API-key integrations are assumed**.
- Other agent/model integrations remain future work.

These notes describe the known working topology, not a tested restoration procedure or a complete deployable Compose bundle. Do not blindly copy outdated Compose examples into production.

## Rebuild checklist

1. Provision Docker Desktop or a compatible container host.
2. Retrieve the compatible Paperclip image and **version-pin it**; verify current official Compose configuration.
3. Restore PostgreSQL data and application data from an actually tested backup before bringing up an existing company instance.
4. Restore session/action signing secrets and other required secure configuration from private secret storage. **Never commit them here.**
5. Set the approved public URL and authenticated deployment mode; configure host exposure and trusted proxy rules as applicable.
6. Verify database migrations, web login, proxy TLS, agent subscriptions, and Paperclip permissions.
7. Apply the CEO charter as standing instructions in the **actual Paperclip agent configuration**; storing `AGENTS.md` in Git does not automatically inject it.
8. Configure and verify usage controls (heartbeats, concurrency, cooldowns, budgets) before enabling automation.
9. Test backups and a complete restoration path; record approved recovery steps.

## Outstanding recovery work

- Export an appropriately redacted copy of the **working** Compose stack and configuration template into this repo.
- Establish storage volume inventories and backup coverage for PostgreSQL and Paperclip state.
- Document private secret storage and recovery ownership, without exposing values.
- Record tested instructions for connecting the CEO charter to the correct Paperclip/Codex runtime.
- Verify trusted reverse-proxy configuration and network access controls.

**No backup, redeployment, or quota restriction is assumed operational merely because it is described here.**
