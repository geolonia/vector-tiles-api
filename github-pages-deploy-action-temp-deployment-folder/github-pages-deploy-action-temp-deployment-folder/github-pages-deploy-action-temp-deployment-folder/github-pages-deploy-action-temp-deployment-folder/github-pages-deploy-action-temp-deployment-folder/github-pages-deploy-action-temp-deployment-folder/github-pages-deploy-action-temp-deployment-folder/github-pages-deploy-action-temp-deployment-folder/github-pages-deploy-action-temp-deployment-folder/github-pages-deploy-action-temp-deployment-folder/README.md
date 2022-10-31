# Vector Tiles API

このリポジトリは、GeoJSON フォーマットのデータを GitHub Actions で Mapbox Vector Tile (`.mvt`) フォーマットに変換し API として公開するためのテンプレートリポジトリです。

Geolonia の Javascript API や、Mapbox GL JS、 MapLibre GL JS では以下のように指定する事でデータを表示することができます。

詳しくは [デモをご参考ください](https://codepen.io/naogify/pen/OJZGRQY) 

```
const map = new geolonia.Map("#map");

map.on("load", () => {

  map.addSource("sample-data", {
    type: "vector",
    url: "https://YOUR-GITHUB-USER.github.io/YOUR-REPOSITORY/tiles/tiles.json",
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
});
```
上記は、Geolonia Javascript API の例になります。


## ご利用方法

* [[Use this template]](https://github.com/naogify/vector-tiles-api/generate) ボタンをクリックして、このテンプレートを自分のリポジトリにコピーしてください。
* [GitHub Pages の設定方法](#github-pages-%E3%81%AE%E8%A8%AD%E5%AE%9A%E6%96%B9%E6%B3%95) を参考に設定をして下さい。
* `example.geojson` を編集してコミットすると数分後に ベクトルタイルが生成されます。
* `https://<あなたのGitHubユーザー名>.github.io/<リポジトリ名>/tiles/tiles.json` の URL を以下のように指定することで、データソースとして地図に追加できます。（[サンプル URL](https://geolonia.github.io/vector-tiles-api/tiles/tiles.json)）
* `source-layer` は、`g-simplestyle-v1` と指定して下さい。

```
map.addSource("sample-data", {
  type: "vector",
  url: "https://YOUR-GITHUB-USER.github.io/YOUR-REPOSITORY/tiles/tiles.json",
});
```


## GitHub Pages の設定方法

* GitHub のリポジトリのメニューの中にある [Settings] をクリックしてください。
* 移動先のページの下の方にある [GitHub Pages] のところで、以下のように設定してください。

![sample](https://user-images.githubusercontent.com/8760841/195016374-3630ae80-b170-4d87-8e3d-88f5408e7a7b.png)

