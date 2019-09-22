# TypeScriptをBabelでES5に変換するやつ

## npm install

```bash
npm install --save-dev \
  @babel/cli \
  @babel/core \
  @babel/preset-env \
  @babel/preset-typescript \
  tslint \
  typescript
```

## workspaceの設定

* babel/tscコマンドが使えるように環境変数のPathに追記

```json
{
	"folders": [{
		"path": "."
	}],
	"settings": {
		"terminal.integrated.env.windows": {
			"PATH": "${env:PATH};${workspaceRoot}\\node_modules\\.bin"
		}
	}
}
```

## TypeScript & Babelの設定ファイル

### babel.config.js

```js
const presets = [
  ["@babel/preset-env"],
  ['@babel/preset-typescript']
];
module.exports = { presets }
```

### tsconfig.json

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "es6",
    "rootDir": "./src"
  }
}
```

## 変換コマンド

* 型チェックはtscでやる

```bash
tsc -noEmit && babel src -x .ts --out-dir dist
```

### `package.json` にコマンドを登録

```json
{
  ...
  "scripts": {
    "dist": "tsc -noEmit && babel src -x .ts --out-dir dist"
  },
  ...
}
```

* 登録したコマンドを使用

```bash
npm run dist
```