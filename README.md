バンドラーに esbuild、CSS プロセッサに Bulma を使ったときの初期設定。

## package.json

```js
{
  "name": "app",
  "private": true,
  "devDependencies": {
    "esbuild": "^0.23.1"
  },
  "scripts": {
    "build": "esbuild app/javascript/*.* --bundle --sourcemap --format=esm --outdir=app/assets/builds --public-path=/assets",
    "build:css": "sass ./app/assets/stylesheets/application.bulma.scss:./app/assets/builds/application.css --no-source-map --load-path=node_modules"
  },
  "dependencies": {
    "@hotwired/stimulus": "^3.2.2",
    "@hotwired/turbo-rails": "^8.0.10",
    "bulma": "^1.0.2",
    "sass": "^1.79.3"
  }
}
```

JS ファイルをバンドル

```js
"build": "esbuild app/javascript/*.* --bundle --sourcemap --format=esm --outdir=app/assets/builds --public-path=/assets",
```

- `app/javascript`: ディレクトリ内のすべてのファイルをバンドル対象にする
- `--bundle`: 依存関係を解決し、1 つのファイルにバンドルする
- `--sourcemap`: ソースマップを生成する。デバッグ時に元のソースコードを参照できる
- `--format=esm`: 出力フォーマットを ES モジュールに設定する
- `--outdir=app/assets/builds`: ビルドしたファイルを`app/assets/builds`ディレクトリに保存する
- `--public-path=/assets`: 出力ファイルの公開パスを`/assets`に設定する。ブラウザがファイルを取得するときの基準となるパス

CSS ファイルをビルド

```js
"build:css": "sass ./app/assets/stylesheets/application.bulma.scss:./app/assets/builds/application.css --no-source-map --load-path=node_modules"
```

- `./app/assets/stylesheets/application.bulma.scss`ファイルをビルドして、`./app/assets/builds/application.css`として出力する


