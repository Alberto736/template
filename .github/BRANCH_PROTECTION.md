# Branch Protection Rules Template

## Main Branch Protection
- **Require pull request reviews before merging**
  - Required approvals: 2
  - Dismiss stale PR approvals when new commits are pushed
  - Require review from CODE OWNERS
  - Restrict reviews to users who have write access

- **Require status checks to pass before merging**
  - Required status checks:
    - `security-scan`
    - `dependency-review`
    - `dependency-inventory`
    - `vulnerability-alert`
    - `dependency-approval`

- **Enforce admin settings**
  - Restrict pushes that create matching branches
  - Require linear history
  - Do not allow bypassing the above settings

## Team Assignments

### Security Team
- **Responsibilities:**
  - Review all dependency updates
  - Approve security-related PRs
  - Monitor vulnerability alerts
  - Maintain security policies

### DevOps Team
- **Responsibilities:**
  - Docker and infrastructure dependencies
  - GitHub Actions updates
  - Terraform module updates
  - CI/CD pipeline dependencies

### Language Teams
- **Python Team:** pip, poetry, conda dependencies
- **JavaScript Team:** npm, yarn dependencies  
- **Java Team:** Maven, Gradle dependencies
- **.NET Team:** NuGet dependencies
- **PHP Team:** Composer dependencies
- **Ruby Team:** RubyGems dependencies

## Approval Matrix

| Dependency Type | Required Reviewers | Auto-Merge |
|----------------|-------------------|------------|
| Patch updates | 1 (language team) | ✅ |
| Minor updates | 2 (language + security) | ❌ |
| Major updates | 3 (language + security + tech-lead) | ❌ |
| Security patches | 1 (security team) | ✅ |
| Docker images | 2 (devops + security) | ❌ |

## Emergency Procedures

### Critical Vulnerability Response
1. **Immediate Action:** Security team creates emergency PR
2. **Fast-Track:** Bypass normal approval process
3. **Deployment:** Auto-merge after security scan passes
4. **Notification:** Alert all teams via Slack

### Rollback Procedures
1. **Identify:** Monitor for breaking changes post-update
2. **Rollback:** Revert to previous working version
3. **Analysis:** Root cause investigation
4. **Prevention:** Update policies to prevent recurrence
