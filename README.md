# GitHub Actions Runner Controller

## 前提条件

https://docs.github.com/ja/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

- [docker](https://docs.docker.com/engine/install/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [helm](https://helm.sh/ja/docs/intro/install/)
- [minikube](https://minikube.sigs.k8s.io/docs/start/)

## 概要

[Actions Runner Controller について](https://docs.github.com/ja/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/about-actions-runner-controller) を参照

## アクション ランナー コントローラーのインストール

[ドキュメント](https://docs.github.com/ja/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller#installing-actions-runner-controller)

```bash
NAMESPACE="arc-systems"
helm install arc \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller
```

## PAT の作成

[ドキュメント](https://docs.github.com/ja/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/authenticating-to-the-github-api#personal-access-token-classic-%E3%81%A7-arc-%E3%81%AE%E8%AA%8D%E8%A8%BC%E3%82%92%E8%A1%8C%E3%81%86)

https://github.com/settings/tokens/new から下記スコープで PAT を作成する

> - リポジトリ ランナー: repo
> - Organization ランナー: admin:org

## ランナー スケール セットの構成

[ドキュメント](https://docs.github.com/ja/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller#configuring-a-runner-scale-set)

```bash
INSTALLATION_NAME="arc-runner-set"
NAMESPACE="arc-runners"
GITHUB_CONFIG_URL="https://github.com/<your_enterprise/org/repo>"
GITHUB_PAT="<PAT>"
helm install "${INSTALLATION_NAME}" \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    --set githubConfigUrl="${GITHUB_CONFIG_URL}" \
    --set githubConfigSecret.github_token="${GITHUB_PAT}" \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set
```

## 参考資料

- https://docs.github.com/ja/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/about-actions-runner-controller
- https://github.com/actions/actions-runner-controller 
- https://zenn.dev/korosuke613/scraps/703218980ddc5d
