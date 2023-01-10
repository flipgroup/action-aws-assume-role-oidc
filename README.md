# Action AWS assume IAM role via OpenID Connect

GitHub Action for assuming an AWS IAM role via a [GitHub OpenID Connect identity provider](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect) (OIDC).

Optionally a second target IAM role can be assumed from the first OIDC enabled role.

## Usage

```yaml
jobs:
  main:
    name: OpenID Connect (OIDC) IAM role
    runs-on: ubuntu-latest
    # note: permissions required to fetch OpenID Connect token and allow actions/checkout
    permissions:
      contents: read
      id-token: write
    steps:
      - name: Assume AWS IAM role
        uses: flipgroup/action-aws-assume-role-oidc@main
        with:
          # note: assume-role-arn is optional
          web-identity-role-arn: arn:aws:iam::ACCOUNT_ID:role/OIDC_TRUSTED_ROLE
          assume-role-arn: arn:aws:iam::ACCOUNT_ID:role/TARGET_ASSUME_ROLE
          aws-region: ap-southeast-2
      - name: whoami
        run: aws sts get-caller-identity
```
