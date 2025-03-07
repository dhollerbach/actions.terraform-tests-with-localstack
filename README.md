# Terraform Tests With LocalStack

GitHub action that runs Terraform tests using LocalStack.

## Inputs

| Name                    | Required     | Description                                                                                                                                                         |
| ----------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `args`                  | **Optional** | Arguments to use when running `terraform init` and `terraform apply`. E.g. `--backend-config=my-config-file.conf --var-file=dev.tfvars -var MY_VARIABLE=some_value`. Defaults to `""`. |
| `github-user`           | **Optional** | The GitHub user to associate with the personal access token. GitHub does not actually use this user so any value will work. Default is `github-user`.               |
| `localstack-api-key`    | **Optional** | The LocalStack API key to use when setting up LocalStack Pro. Set **localstack-use-pro** to `true` if setting your api key.                                         |
| `localstack-image-tag`  | **Optional** | The LocalStack image tag to use when setting up LocalStack. Defaults to `latest`.                                                                                   |
| `localstack-use-pro`    | **Optional** | Whether or not to use LocalStack Pro. If using LocalStack Pro, set to `true` and set **localstack-api-key** to your LocalStack API key. Defaults to `false`.        |
| `personal-access-token` | **Optional** | The GitHub personal access token to use when running `terraform init`. Specify if any modules are stored in private GitHub repositories.                            |
| `run-apply`             | **Optional** | Whether or not to run `terraform apply --auto-approve`. Default is `true`.                                                                                          |
| `run-formatter`         | **Optional** | Whether or not to run `terraform fmt -recursive`. Default is `true`.                                                                                                |
| `run-linter`            | **Optional** | Whether or not to run `tflint --recursive`. Default is `true`.                                                                                                      |
| `run-security-scanner`  | **Optional** | Whether or not to run `tfsec`. Default is `true`.                                                                                                                   |
| `run-validator`         | **Optional** | Whether or not to run `terraform validate`. Default is `true`.                                                                                                      |
| `terraform-version`     | **Optional** | The Terraform version to setup. Required if Terraform is not previously setup.                                                                                      |
| `terraform-wrapper`     | **Optional** | Whether or not to enable to Terraform wrapper when setting up Terraform. Defaults to `false`.                                                                       |
| `working-directory`     | **Optional** | The working directory to run tests in. Default is the current directory.                                                                                            |

## Example Usage

### Basic

```yaml
- name: Run Terraform Tests with LocalStack
  uses: dhollerbach/actions.terraform-tests-with-localstack@v1
  with:
    run-formatter: true
    run-linter: true
    run-security-scanner: true
    run-apply: true
    terraform-version: 1.11.0
```

### LocalStack Pro

```yaml
- name: Run Terraform Tests with LocalStack
  uses: dhollerbach/actions.terraform-tests-with-localstack@v1
  with:
    localstack-api-key: ${{ secrets.LOCALSTACK_API_KEY }}
    localstack-use-pro: true
    run-formatter: true
    run-linter: true
    run-security-scanner: true
    run-apply: true
    terraform-version: 1.11.0
```
