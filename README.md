# Vector Tiles API

このリポジトリは、GeoJSON フォーマットのデータを GitHub Actions で ベクトルタイル に変換し API として公開するためのテンプレートリポジトリです。

Geolonia の Javascript API や、Mapbox GL JS、 MapLibre GL JS では以下のように指定する事でデータを表示することができます。

詳しくは [デモをご参考ください](https://codepen.io/naogify/pen/poVQGyQ) 

```
const map = new geolonia.Map("#map");

map.on("load", () => {
  map.addSource("sample-data", {
    type: "vector",
    tiles: ["https://YOUR-GITHUB-USER.github.io/vector-tiles-api/tiles/{z}/{x}/{y}.mvt"],
  });

  map.addLayer({
    id: "sample-layer",
    source: "sample-data",
    "source-layer": "g-simplestyle-v1",
    type: "fill",
    paint: {
      "fill-color": "#ff0000",
    }
  });
```
上記は、Geolonia Javascript API の例になります。


## ご利用方法

* [[Use this template]](./vector-tiles-api/generate) ボタンをクリックして、このテンプレートを自分のリポジトリにコピーしてください。
* `example.geojson` を編集してコミットすると数分後に ベクトルタイルが生成されます。
* `https://<あなたのGitHubユーザー名>.github.io/<リポジトリ名>/tiles/{z}/{x}/{y}.mvt` の URL を以下のように指定することで、データソースとして地図に追加できます。
* `source-layer` は、`g-simplestyle-v1` と指定して下さい。

```
map.addSource("sample-data", {
  type: "vector",
  tiles: ["https://YOUR-GITHUB-USER.github.io/vector-tiles-api/tiles/{z}/{x}/{y}.mvt"],
});
```


## GitHub Pages の設定方法

* GitHub のリポジトリのメニューの中にある [Settings] をクリックしてください。
* 移動先のページの下の方にある [GitHub Pages] のところで、以下のように設定してください。

![sample](https://user-images.githubusercontent.com/8760841/195016374-3630ae80-b170-4d87-8e3d-88f5408e7a7b.png)

