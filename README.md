# GitHub を活用したベクトルタイル配信基盤

このリポジトリは、`CSV` と `GeoJSON` フォーマットのデータを Mapbox Vector Tile (`.mvt`) フォーマットに変換し API として公開するための**テンプレートリポジトリ**（後述）です。

地理空間情報を含む CSV または GeoJSON をコミットすると、 .mvt が作成され、同レポジトリの GitHub Pages 上にホストされます。ホストされたデータへ、空間IDタイルデータ取得SDKや、Mapbox GL JS、 MapLibre GL JS、Geolonia の Javascript API等を用いてアクセスすることで、 API 配信基盤として機能します。

開発者が、自治体が公開するオープンデータや自組織が保有する地理空間情報を 空間ID のAPI化するために提供しています。

**テンプレートレポジトリ**とは、既存のレポジトリを自身や他の人が同じディレクトリ構造や GitHub Actions 等を持つ新たなレポジトリを作ることができる仕組みです。フォークとは異なり、ひとつのテンプレートレポジトリから、複数の、異なる名前とURLを持つレポジトリを作成することできます。

![Geolonia spatialid-gh-template-image](https://user-images.githubusercontent.com/1124652/198641609-c585dc85-e045-4fcf-89c3-e4adfd0bcfb4.jpg)

## テンプレートレポジトリの利用方法

* [[Use this template]](https://github.com/geolonia/vector-tiles-api/generate) ボタンをクリックして、このテンプレートを自分のリポジトリにコピーしてください。
* [GitHub Pages の設定方法](#github-pages-%E3%81%AE%E8%A8%AD%E5%AE%9A%E6%96%B9%E6%B3%95) を参考に設定をして下さい。
* `example.csv` を編集してコミットすると数分後に ベクトルタイルが生成されます。
  * csv の先頭行には、**必ず `緯度`、`経度`という項目を追加して下さい**
  * 任意のファイル名の CSV を1つのみ設置できます。
* `https://<あなたのGitHubユーザー名>.github.io/<リポジトリ名>/tiles/tiles.json` の URLが生成されます。（[サンプル URL](https://geolonia.github.io/vector-tiles-api/tiles/tiles.json)）

### 空間IDタイルデータ取得SDKのご利用方法

以下の公式ドキュメントをご参考ください。  
https://github.com/geolonia/spatial-id-request-sdk/blob/main/README.md

### 生成したデータを地図に表示する

また、[GitHub を活用した空間ID API を使って港区のフリーWi-Fiスポットを地図に表示するサンプル](https://codepen.io/shinichin/pen/PoaqQKm) では、作成した港区が公開している公衆無線LANのアクセスポイントのオープンデータを、地図（ここでは、[Geolonia Maps](https://geolonia.com/maps/)）の上に表示させています。

![スクリーンショット 2022-10-29 0 16 31](https://user-images.githubusercontent.com/1124652/198672850-55ec7a2f-8d08-43ff-8594-dd0619f70e04.png)


### GeoJSON データのご利用方法

* 以下の [build.yml](https://github.com/geolonia/vector-tiles-api/blob/main/.github/workflows/build.yml#L20) の 20行目の `"*.csv"` を `"*.geojson"` に書き換えて push して下さい。
* `example.csv` を削除し、`example.geojson` をアップロードして下さい。数分でタイルが生成されます。

**build.yml**
```
  with:
    file: "*.csv"
    out_dir: ./
```

https://github.com/geolonia/vector-tiles-api/blob/main/.github/workflows/build.yml#L20

## GitHub Pages の設定方法

* GitHub のリポジトリのメニューの中にある [Settings] をクリックしてください。
* 移動先のページの下の方にある [GitHub Pages] のところで、以下のように設定してください。

![sample](https://user-images.githubusercontent.com/8760841/195016374-3630ae80-b170-4d87-8e3d-88f5408e7a7b.png)

## データ出典

サンプルデータは以下のデータを利用しています。
- 「 公衆無線LANアクセスポイント一覧」（港区）（https://opendata.city.minato.tokyo.jp/dataset/minato_city_wifi/resource/d02ec3d4-7c47-4538-bdf8-05167c5f7112) を加工して作成
