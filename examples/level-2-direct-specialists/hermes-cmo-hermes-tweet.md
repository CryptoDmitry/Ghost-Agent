# Level 2 Direct Specialist: hermes-cmo With Hermes Tweet

This example documents a marketing specialist that uses Hermes Tweet for X/Twitter research, reading, and gated publishing.

## Agent Inventory

- Agent name: `hermes-cmo`
- Level: 2 direct specialist
- Primary role: monitor market conversations, draft posts, and report campaign signals.
- Runtime: Hermes Agent
- Optional plugin: Hermes Tweet
- Plugin source: `https://github.com/Xquik-dev/hermes-tweet`

## Skill Placement

Install Hermes Tweet in the specialist runtime, not in the Control Room. Keep this repo as the control plane.

```text
/srv/hermes-cmo/data
  .env
  skills/
    hermes-tweet/
```

## Environment Map

Record secret names only. Do not copy raw values into the Control Room.

| Name | Scope | Location | Required |
| --- | --- | --- | --- |
| `XQUIK_API_KEY` | read tools | specialist runtime env | yes for `tweet_read` |
| `HERMES_TWEET_ENABLE_ACTIONS` | write gate | specialist runtime env | yes for `tweet_action` |

## Safe Use

- Use `tweet_explore` for offline planning before credentials are configured.
- Use `tweet_read` only after `XQUIK_API_KEY` is present.
- Keep `tweet_action` disabled until the operator sets `HERMES_TWEET_ENABLE_ACTIONS=true`.
- Put approval rules in the agent runbook before any posting workflow.
- Store only secret names, scopes, and rotation notes in this repo.

## Example Runbook Entry

```text
Daily marketing scan:
1. Review saved audiences and tracked topics with tweet_read.
2. Summarize notable posts, accounts, and wording patterns.
3. Draft response ideas in the Control Room notes.
4. Request operator approval before any tweet_action call.
```

## Recovery Notes

If the specialist loses access, disable `HERMES_TWEET_ENABLE_ACTIONS`, rotate the API key outside this repo, and update the secret map with the new rotation date only.
