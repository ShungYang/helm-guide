# Helm Charts

> Helm uses a packaging format called charts.

A chart is a collection of files that describe a related set of Kubernetes resources.

## Topics

* 建立初始化一個 helm chart.
* helm chart 的目錄結構.
* 將 helm chart 發佈到 Nexus private repository.

## Initial a chart

```
helm create demo-chart
```

## The Chart File Structure

/demo-chart

* [Chart.yaml](https://helm.sh/docs/topics/charts/#the-chartyaml-file) : A YAML file containing information about the chart
* values.yaml : The default configuration values for this chart
* charts/ : A directory containing any charts upon which this chart depends
* templates/ : A directory of templates that, when combined with values, will generate valid Kubernetes manifest files.
* templates/tests : Validate that your configuration from the values.yaml file was properly injected (use `helm test {chart}`)

## Publish chart to Nexus private repository

* 編寫好你要的 chart 後先確認 helm render 出你要的結果

```
helm template demo-chart --debug
```

* 將 helm chart 打包成 `tar檔`

```
helm package ./demo-chart --version=1.1
```

* 將 chart 推送到 private repository

```bash
curl -u {name}:{pwd} https://nexus.mic.com.tw/repository/helm-hosted-demo/ --upload-file demo-chart-1.1.tgz -v
```

## Reference Link

* [How to Helm With Sonatype Nexus](https://betterprogramming.pub/how-to-helm-with-sonatype-nexus-c49c98324a19) by Gaurav Agarwal
* [將打包好的 Helm Chart Push 至 Nexus](https://blog.yowko.com/helm-push-nexus/) by Yowko Tsai

__Enjoy!__
