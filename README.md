# helm-guide

> The package manager for Kubernetes

## Helm Charts

> Helm uses a packaging format called charts.

A chart is a collection of files that describe a related set of Kubernetes resources.

## Prerequisites

* 請先建立一個 Kubernetes Cluster, 之後我們就透過 helm 做服務的佈署及後續的管理.
* 安裝 kubectl, 並確認 `~/.kube/config` 存在且配置正確.

## Install Helm

我們需要安裝 Helm CLI, 我的伺服器作業系統是 Ubuntu 所以我是透過 `Snap` 進行安裝.

```bash
sudo snap install helm --classic
```

其他作業系統的安裝方式可以參考[官方文件](https://helm.sh/docs/intro/install/)

## Getting started

* 如何 Create Helm chart and publish to nexus repository 可以[參考](https://github.com/ShungYang/helm-guide/blob/master/README-chart.md).

安裝好 Helm CLI 後, Helm 使用的是 `~/.kube/config` 的群集設定, 接下來會介紹一些比較常用的指令

* 先添加建立的 private nexus helm demo repo

```
helm repo add nexus-helm-hosted-demo https://nexus.mic.com.tw/repository/helm-hosted-demo/ --username {name} --password {pwd}
```

* 更新 helm 清單中的 repository (預設會包含官方的儲存庫)到最新.

```
helm repo update
```

* 查看 nexus-helm-hosted-demo 中有哪些 charts.

```
helm search repo nexus-helm-hosted-demo
```

* Fetch the latest chart

```
helm fetch nexus-helm-hosted-demo/demo-chart
```

* 下載一個遠端的 charts 到本地端, 下載後可以看到一個 `tar` 檔, 檔名帶著 chart version, 解壓縮可以看到內容.

```
helm pull nexus-helm-hosted-demo/demo-chart
tar xvf demo-chart-1.1.tgz
```

* 安裝本地端的 charts 並佈署 helm charts 到當前使用的 context, 此時該服務稱為一個 `Release`, 當我們 repeat 這個安裝指令後, 又會多出一個 Release

```
helm install demo-app ./demo-chart --debug
```

* 也可直接安裝遠端的 charts.

```
helm install demo-app nexus-helm-hosted-demo/demo-chart --debug
```

* 查看當前使用 Helm CLI 佈署了哪些 Releases.

```
helm list
```

* 確認指定 Release 的當前狀態.

```
helm status demo-app
```

* 使用本地端的 chart 更新 Release

```
helm upgrade demo-app ./demo-chart --debug
```

* 將 Release 退到指定的版本

```
helm rollback demo-app 1
```

* 顯示 Release 的版本歷程

```
helm history demo-app
```

* 解安裝佈署的 Release

```
helm uninstall
```

## Reference Link

* [Quickstart Guide](https://helm.sh/docs/intro/quickstart/)

__Enjoy!__
