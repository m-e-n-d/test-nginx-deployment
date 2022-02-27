# test-nginx-deployment
Kubernetes上でとりあえず色々な動作確認をできるようにnginxのPodをデプロイするためのmanifestです。
同じような内容のdeploymentを二つ作成し、2つのPodの動作を比較できるようにしています。

## ファイル構造
```
.
├── README.md               //このファイル
└── manifests
    ├── deployment_a.yml    //aのnginxのdeploymentを記載したmanifest
    ├── deployment_b.yml    //bのnginxのdeploymentを記載したmanifest
    ├── namespace.yml       //nginxを配置するnamespaceを記載したmanifest
    └── service.yml         //それぞれのnginxへのアクセスを定義するserviceのmanifest

```

## 使い方

```shell
$ kubectl apply -f manifests
```

## 作成されるリソース

- deployment
    - Aのnginxのdeployment
    - Bのnginxのdeployment
- namespace
    - test-nginxという`namespace`を作成します。
- service
    - それぞれのPodにアクセスできるserviceを作成します。
    - 8080番ポートでserviceを作成します。
    - クラスター外からアクセスしたい場合は`kubectl port-forward`でアクセスできるようになります。

## アクセス確認
```shell
$ kubectl port-forward -n test-nginx svc/test-nginx-service 8080:8080
```
