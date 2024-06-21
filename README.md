# udemy-ml-regression


## Dockerの実行手順

- `Dockerfile`を指定して、imageをビルドします。

```sh
# ビルド
$ docker build --platform linux/amd64 -t udemy-ml-regression:1.0.0 -f Dockerfile .
```

- imageを指定してコンテナを起動、Jupyter Labを実行します。サンプルコードのNotebookを`-v`でコンテナにマウントします。

```sh
# コンテナ起動＋Jupyter Lab実行
$ docker run -it --rm --name udemy-ml-regression -v $PWD:/opt -p 8888:8888 udemy-ml-regression:1.0.0 jupyter lab --ip=0.0.0.0 --allow-root --NotebookApp.token='' --port=8888
```

- webブラウザのURL http://localhost:8888 にアクセスし、サンプルコードを実行します。

- 利用終了時はコマンドラインで Ctrlキー + C を押下して、Jupyter Labを停止してください。