# ClawHub Search + Ranking Workflow

## Discovery URLs

- Search entry: `https://clawhub.ai/skills?focus=search`
- Stars ranking: `https://clawhub.ai/skills?sort=stars&dir=desc`
- Recently updated: `https://clawhub.ai/skills?sort=updatedAt&dir=desc`

## Practical Search Flow

1. Run Q1 broad query to collect capability families.
2. Run Q2 scenario query to narrow to user workflow.
3. Run Q3 failure query with exact error markers.
4. Merge candidates and deduplicate by slug.
5. Rank with weighted scoring.

## Weighted Scoring (100)

- Goal fit: 40
- Failure-type fit: 25
- Setup friction: 15
- Maintenance/activity: 10
- Safety/risk posture: 10

## Recommendation Guardrails

- Prefer lower-friction options when scores are close.
- Flag skills requiring broad scopes or paid APIs.
- Include one conservative fallback for reliability.
- Avoid recommending >3 primary options.
