# Security and data handling

Never publish API keys, customer transcripts or provider credentials. Use synthetic examples in issues. If you discover a security concern, avoid posting exploitation details publicly; contact the maintainer through a private channel listed on their GitHub profile. No dedicated security mailbox is configured.

The application does not intentionally persist API keys, notes or results. Live requests share input with TypeSafe through the application server. Hosting/provider logs and retention must be assessed independently. The development server binds to all interfaces; use it only in a trusted local environment.

Routing labels do not grant permissions or perform actions. Model outputs are advisory and require workflow-specific validation.
