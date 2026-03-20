# gitlab

## add k3s cluster to gitlab as runner

install Helm on the master node

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

get your GitLab Runner Token

- go to your project (or group) on GitLab.com.
- navigate to Settings > CI/CD > Runners.
- click New project runner, add any tags you want, and click Create.
- gitLab will provide a Runner Authentication Token (it usually starts with glrt-). Copy this.


create a `values.yaml` file with the following content, replacing `<YOUR_GITLAB_RUNNER_TOKEN>` with the token you copied from GitLab:

```yaml
gitlabUrl: "https://gitlab.com/"
runnerRegistrationToken: "" # Leave empty, we use runnerToken now
runnerToken: "<YOUR_TOKEN>"
concurrent: 4 # How many jobs can run at once

rbac:
  create: true

runners:
  config: |
    [[runners]]
      [runners.kubernetes]
        namespace = "{{.Release.Namespace}}"
        image = "ubuntu:22.04"
```

deploy the runner using Helm:

```bash
# Add the GitLab chart repository
helm repo add gitlab https://charts.gitlab.io
helm repo update

# Create a namespace for the runner
kubectl create namespace gitlab-runner

# Install the runner using your values.yaml
helm install --namespace gitlab-runner gitlab-runner -f values.yaml gitlab/gitlab-runner
```