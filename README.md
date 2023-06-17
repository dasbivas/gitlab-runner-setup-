# Gitlab-Runner for Ubuntu
```
apt insall docker.io
sudo curl -L --output /usr/local/bin/gitlab-runner "https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64"
sudo chmod +x /usr/local/bin/gitlab-runner
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start
```
# Gitlab-Runner /etc/gitlab-runner/config.toml

```
volumes = ["/var/run/docker.sock:/var/run/docker.sock", "/certs/client", "/cache"]
```
# Gitlab-Runner image pull from Private Registry # CICD Variable
```
 printf "my_username:my_password" | openssl base64 -A
```
# CICD Variable Name 
```
DOCKER_AUTH_CONFIG
```
```
{
    "auths": {
        "registry.gitlab.com:5000": {
            "auth": "bXlfdXNlcm5hbWU6bXlfcGFzc3dvcmQ="
        }
    }
}
```
# .gitlab-ci-sample
```
image: registry.gitlab.com/tdc4/environment-images:latest
services:
  - docker:19.03-dind
stages:
  - mirror
before_script:
  - echo -n $CI_JOB_TOKEN | docker login -u gitlab-ci-token --password-stdin $CI_REGISTRY
mirror:
  stage: mirror
  tags: 
    - internet
  script:
  - echo "abc"
```
#