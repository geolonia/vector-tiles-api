# Vector Tiles API

このリポジトリは、`CSV`や`GeoJSON` フォーマットのデータを GitHub Actions で Mapbox Vector Tile (`.mvt`) フォーマットに変換し API として公開するためのテンプレートリポジトリです。
生成したタイルは、空間IDタイルデータ取得SDKや、Mapbox GL JS、 MapLibre GL JS、Geolonia の Javascript API等でご利用いただけます。

* [空間IDタイルデータ取得SDKのデモ](https://geolonia.github.io/spatial-id-request-sdk/)
* [Geolonia Javascript API を使用して地図を表示するデモ](https://codepen.io/naogify/pen/OJZGRQY) 


## ご利用方法

* [[Use this template]](https://github.com/naogify/vector-tiles-api/generate) ボタンをクリックして、このテンプレートを自分のリポジトリにコピーしてください。
* [GitHub Pages の設定方法](#github-pages-%E3%81%AE%E8%A8%AD%E5%AE%9A%E6%96%B9%E6%B3%95) を参考に設定をして下さい。
* `example.csv` を編集してコミットすると数分後に ベクトルタイルが生成されます。
  * csv の先頭行には、**必ず `緯度`、`経度`という項目を追加して下さい**
  * 任意のファイル名の CSV を1つのみ設置できます。
* `https://<あなたのGitHubユーザー名>.github.io/<リポジトリ名>/tiles/tiles.json` の URLが生成されます。（[サンプル URL](https://geolonia.github.io/vector-tiles-api/tiles/tiles.json)）



### 空間IDタイルデータ取得SDKのご利用方法

以下の公式ドキュメントをご参考ください。  
https://github.com/geolonia/spatial-id-request-sdk/blob/main/README.md


### Mapbox GL JS 等のラリブラリでのご利用方法

生成した `tiles.json` の URL を以下のように指定することで、データソースとして地図に追加できます。

* `source-layer` は、`g-simplestyle-v1` と指定して下さい。

```
const map = new geolonia.Map({
  container: "#map",
  center: [139.73807, 35.65118],
  zoom: 13,
});

map.on("load", () => {

  map.addSource("sample-data", {
    type: "vector",
    url: "https://YOUR-GITHUB-USER.github.io/YOUR-REPOSITORY/tiles/tiles.json",
  });

  map.addLayer({
    id: "circle",
    source: "my-data",
    "source-layer": "g-simplestyle-v1",
    type: "circle",
    paint: {
      "circle-color": "#ff0000",
      "circle-opacity": 0.5,
      "circle-radius": 20
    },
    layout: {}
  });
});
```
上記は、Geolonia Javascript API の例になります。

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
