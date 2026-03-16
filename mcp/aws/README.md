# mcp/aws/

AWS MCP server for cloud resource interaction — querying, inspecting, and
managing AWS resources from within an agent session.

## Setup

```bash
# Requires uv / uvx installed, and AWS credentials configured locally.
# Replace YOUR_PROFILE_NAME and YOUR_REGION in your local config.
# Never commit real profile names, regions, or account IDs here.

# Verify credentials before use:
aws sts get-caller-identity --profile YOUR_PROFILE_NAME
```

## Notes

- Use a dedicated IAM role with least-privilege permissions scoped to the
  tasks you intend the agent to perform. Never use root credentials.
- Prefer named profiles over environment variable credentials for
  auditability — it's easier to see which identity the agent is assuming.
- See `infrastructure/aws-iam/` for role setup patterns.
