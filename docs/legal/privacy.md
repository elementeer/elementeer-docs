# Privacy Policy

*This is a placeholder privacy policy. Replace with your actual privacy policy before publishing.*

## Data Collection

Elementeer does not collect, store, or transmit data from your WordPress site to external servers. All operations occur within your infrastructure — the MCP server runs on your machine, and the WordPress plugin runs on your server.

## What Elementeer Accesses

The Elementeer WordPress plugin accesses:

- WordPress site data (posts, pages, media, users, settings)
- Elementor data (templates, kits, global styles, widgets)
- Plugin data for detected integrations (WooCommerce, Voxel, booking systems, etc.)

This data is accessed only to fulfill API requests from authenticated MCP servers. It is not logged, stored externally, or transmitted to third parties.

## API Keys

API keys are stored in your WordPress database. The MCP server stores configuration (site URLs, API keys) in `~/.elementeer/config.json` on your local machine. You are responsible for securing this file — it contains credentials that grant access to your WordPress site.

## Third-Party Services

Elementeer's Free tier does not connect to any external services. The MCP server communicates only with your configured WordPress sites.

The Advanced tier (`@elementeer/pro`) may optionally integrate with:
- AI translation services (for batch translation features)
- AI image generation services (for image creation features)

These integrations are opt-in and require separate configuration. Data is transmitted only when you explicitly invoke those features.

## Logging

The MCP server logs operational data locally (tool invocations, response times, errors). These logs are stored on your machine and are not transmitted externally. Log level is configurable via the `ELEMENTEER_LOG_LEVEL` environment variable.

## Your Responsibilities

- Secure your API keys. Anyone with a valid key can access your site through Elementeer.
- Review the governance model. L2 and L3 operations are queued for your approval — you control what changes are applied.
- If using Advanced tier features with third-party AI services, review those services' privacy policies.

## Contact

For privacy-related questions, contact [privacy@elementeer.xyz](mailto:privacy@elementeer.xyz).
