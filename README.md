# alias.toml

Vote accounts grouped by shared keys: the same withdraw authority, the same signers in the
withdraw multisigs, or identity keys recorded on the same hosts in the IP-change history.

Maintained by ART3MIS.CLOUD - https://art3mis.cloud

- ART3MIS.CLOUD identity `GwHH8ciFhR8vejWCqmg8FWZUCNtubPY2esALvy5tBvji`,
  vote `3iPuTgpWaaC6jYEY7kd993QBthGsQTK3yPCrNJyPMhCD`
- Contact: team@art3mis.cloud, PGP `8E5DAE8C18B42016E27207B95C6631681B91055A`
- Source: https://github.com/a3mc/valias

All data in this file is collected and maintained by ART3MIS.CLOUD. The IP-change history behind
every "Common operation" entry comes from the BigBrother engine (https://bigbrother.art3mis.cloud);
withdraw authorities and multisig signers are read from chain. Keep the header of `alias.toml` in
every copy of the file.

## Format

One file: `alias.toml`. Two entry types, each with its own metadata.

`[[group]]`: vote accounts that share keys or hosts. `anchor` is the vote account the group is
named after (its on-chain name is used); `votes` lists the others.

```toml
[[group]]
anchor = "ANCHOR_VOTE_ACCOUNT"
votes = ["MEMBER_VOTE_ACCOUNT", "MEMBER_VOTE_ACCOUNT"]
[group.metadata]
level = "warning"
info = "Common control: one withdraw authority for all 3"
details = "What was recorded: keys, addresses, dates, counts"
sources = ["https://..."]
```

`[[validator]]`: an entry about one vote account. It is separate from any group the vote
account belongs to and never changes the group's entry.

```toml
[[validator]]
vote = "VOTE_ACCOUNT"
[validator.metadata]
level = "note"
info = "..."
sources = ["https://..."]
```

## Metadata

Same fields for `[[group]]` and `[[validator]]` entries:

| Field | Required | Content |
|---|---|---|
| `level` | yes | `warning`, `note` or `info` (one lowercase word a-z, 16 max) |
| `info` | yes | one line, 120 characters max |
| `details` | no | one paragraph without line breaks, 500 characters max |
| `sources` | no | non-empty list of `https://` links (300 characters max each) where anyone can see the same data |
| `credit` | no | who first reported the finding, 120 characters max |
| `other` | no | e.g. `website`: text or a non-empty list of texts, 500 characters max each; name in lowercase letters, digits and `_`, 32 max |

Plain text only: no control or invisible characters, no nested tables. At most 10 extra fields
per entry and 20 items per list.

The `info` line of a group starts with one of three phrases:

| Phrase | Meaning |
|---|---|
| `Common control:` | one key controls the vote accounts: the same withdraw authority, or shared signers in the multisigs that hold it |
| `Common operation:` | the identity keys were recorded on the same hosts in turn, or one identity on another's host |
| `One operator, declared:` | the operator states it: the same website or company name in validator-info, or a public announcement |

`details` states only what was recorded: keys, addresses, dates and counts.

## Levels

| Level | Use |
|---|---|
| `warning` | the link is not stated by the operator, and the members carry different names, or an unnamed vote account receives stake from open delegation programs |
| `note` | a known operator, or a link the operator states itself |
| `info` | a known arrangement, e.g. a client team's canary nodes |

## Rules

- Vote accounts only, not identity keys.
- A vote account belongs to at most one group. Do not repeat the anchor in `votes`.
- One `[[validator]]` entry per vote account.
- State only what can be checked from the listed sources.
- No personal data. Everything in this file is public.

## Contributing

Open a pull request that edits `alias.toml`, one entity per pull request. Explain in the
description what each source shows. Entries that cannot be checked from their sources are not
merged.

## Acknowledgements

Matching vote accounts by their withdraw authorities and by the signers of their withdraw
multisigs was first reported by Andrei Vacariu (x.com/andreivacariu_, Gossipwatch at
gossip.solstack.app).

## License

MIT
