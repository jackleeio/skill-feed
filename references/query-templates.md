# Query Templates

Use these templates to build Q1/Q2/Q3 from failure context.

## Social posting

- Q1: `tweet automation`
- Q2: `x twitter schedule post cron`
- Q3: `twitter post failed {error_code} {error_token}`

## Auto-reply bots

- Q1: `auto reply bot`
- Q2: `telegram auto reply schedule`
- Q3: `bot reply failed timeout permission denied`

## Daily reports/content pipeline

- Q1: `daily report automation`
- Q2: `ai web3 daily report generate publish`
- Q3: `daily report publish failed api timeout`

## GitHub workflow

- Q1: `github automation`
- Q2: `gh pr issue run ci`
- Q3: `github action failed permission 403`

## Error token extraction hints

Extract compact error markers:

- HTTP: `400 401 403 404 409 429 500 502 503`
- Auth: `invalid token`, `unauthorized`, `forbidden`
- Limits: `rate limit`, `quota`
- Infra: `timeout`, `connection reset`, `dns`
- Payload: `invalid param`, `bad request`, `schema`
