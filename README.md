# udemy-ml-regression
実行環境の環境構築とサンプルコードの実行手順を記載します。

## ライブラリのバージョン
ライブラリはコンテンツ作成時点の[Google Colaboratory](https://colab.google/)の最新バージョンになります。Colabのライブラリは定期的に更新するので、プログラム実行時にエラーが発生する場合、以下のバージョンに戻してください。また、Dockerの実行環境でも以下のバージョンを使用します。
- Python 3.10.12
- pandas 2.0.3
- numpy 1.25.2
- matplotlib 3.7.1
- seaborn 0.13.1
- scikit-learn 1.2.2
- graphviz 0.20.3
- lightgbm 4.1.0
- jupyterlab 4.1.5
- shap 0.41.0
- xgboost 2.0.3
- optuna 3.1.1
- japanize-matplotlib 1.1.3

## Google Colaboratoryの実行環境
[Google Colaboratory](https://colab.google/)はクラウド環境でNotebookを提供します。リンク先にアクセスすると環境構築済みの実行環境を利用できます。

## Dockerコンテナの基本操作
- ubuntuのイメージを使って、コンテナの動きを確認します。
```sh
# コンテナの起動
docker run -it -w /opt ubuntu:latest bash

# マウントしてコンテナ起動
docker run -it -w /opt -v $PWD:/opt ubuntu:latest bash

# マウントしてコンテナ起動、コンテナ自動削除
docker run --rm -it -w /opt -v $PWD:/opt ubuntu:latest bash
```

## Dockerコンテナの実行環境
- コマンドラインでリポジトリをgit cloneし、ディレクトリ`udemy-ml-regression`に移動します。
```sh
# リポジトリの取得
$ git clone https://github.com/ayukat1016/udemy-ml-regression.git

# ディレクトリの移動
$ cd udemy-ml-regression/

# ディレクトリの確認(`/xxx/work`はユーザにより異なります。)
$ pwd
/home/xxx/work/udemy-ml-regression

# ファイルの確認
$ ls
Dockerfile  README.md  notebook  poetry.lock  pyproject.toml  requirements.txt
```

- `Dockerfile`を指定して、imageをビルドします。

```sh
# ビルド
$ docker build --platform linux/amd64 -t udemy-ml:1.0.0 -f Dockerfile .

# ビルドしたイメージの確認
$ docker images
REPOSITORY  TAG    IMAGE ID       CREATED         SIZE
udemy-ml    1.0.0  dc9d49408715   5 days ago      1.62GB
```

- imageを指定してコンテナを起動、Jupyter Labのコマンドを実行します。サンプルコードのNotebookを`-v`でコンテナにマウントします。

```sh
# コンテナ起動＋Jupyter Lab実行
$ docker run -it --rm --name udemy-ml -v $PWD:/opt -p 8888:8888 udemy-ml:1.0.0 jupyter lab --ip=0.0.0.0 --allow-root --NotebookApp.token=''
```

- webブラウザのURL http://localhost:8888 にアクセスし、サンプルコードを実行します。

- 利用終了時はコマンドラインで Ctrlキー + C を押下して、Jupyter Labを停止してください。