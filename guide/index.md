# はじめに

<audio id="vite-audio">
  <source src="/vite.mp3" type="audio/mpeg">
</audio>

## 概要

Vite（フランス語で「素早い」という意味の単語で `/vit/`<button style="border:none;padding:3px;border-radius:4px;vertical-align:bottom" id="play-vite-audio" onclick="document.getElementById('vite-audio').play();"><svg style="height:2em;width:2em"><use href="/voice.svg?no-inline#voice" /></svg></button> ヴィートのように発音）は、現代の Web プロジェクトのために、より速く無駄のない開発体験を提供することを目的としたビルドツールです。2 つの主要な部分で構成されています:

- 非常に高速な [Hot Module Replacement (HMR)](./features#hot-module-replacement) など、[ネイティブ ES モジュール](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules)を利用した[豊富な機能拡張](./features)を提供する開発サーバー。

- [Rollup](https://rollupjs.org) でコードをバンドルするビルドコマンド。プロダクション用に高度に最適化された静的アセットを出力するように事前に設定されています。

Vite はすぐに使える実用的なデフォルトが付属しています。[特徴ガイド](./features)で何ができるかをお読みください。フレームワークや他のツールとの統合は[プラグイン](./using-plugins)を通じて可能です。[設定セクション](../config/)では、必要に応じて Vite をプロジェクトに適合させる方法について説明します。

Vite は完全な型サポートのある [Plugin API](./api-plugin) と [JavaScript API](./api-javascript) によって高い拡張性もあります。

プロジェクトの背景にある基本原理について、[Vite を使う理由](./why) セクションで詳しく知ることができます。

## ブラウザー対応

開発中、Vite はモダンブラウザーが使用され、最新の JavaScript および CSS 機能のほとんどをサポートしていることを前提としています。そのため、Vite は [`esnext` を変換ターゲットとして](https://esbuild.github.io/api/#target)設定します。これによりシンタックスの低下を防ぎ、Vite が元のソースコードにできるだけ近いモジュールを提供できるようになります。Vite は開発サーバーを動作させるためにいくつかのランタイムコードを注入します。これらのコードは、各メジャーリリース時点の [Baseline](https://web-platform-dx.github.io/web-features/) Newly Available に含まれる機能を使用します (このメジャーリリースでは 2025-05-01)。

本番ビルドの場合、Vite はデフォルトで [Baseline](https://web-platform-dx.github.io/web-features/) Widely Available ブラウザーをターゲットとします。これらは少なくとも 2.5 年以上前にリリースされたブラウザーです。ターゲットは設定によって下げることができます。さらに、レガシーブラウザーは公式の [@vitejs/plugin-legacy](https://github.com/vitejs/vite/tree/main/packages/plugin-legacy) を通じてサポートできます。詳細については、[本番環境用のビルド](./build)セクションを参照してください。

## Vite をオンラインで試す {#trying-vite-online}

[StackBlitz](https://vite.new/) で Vite をオンラインで試すことができます。Vite ベースのビルドセットアップをブラウザー上で直接実行するので、ローカルセットアップとほぼ同じですが、マシンに何もインストールする必要がありません。`vite.new/{template}` に移動して、使用するフレームワークを選択できます。

サポートされているテンプレートのプリセットは次のとおりです:

|             JavaScript              |                TypeScript                 |
| :---------------------------------: | :---------------------------------------: |
| [vanilla](https://vite.new/vanilla) | [vanilla-ts](https://vite.new/vanilla-ts) |
|     [vue](https://vite.new/vue)     |     [vue-ts](https://vite.new/vue-ts)     |
|   [react](https://vite.new/react)   |   [react-ts](https://vite.new/react-ts)   |
|  [preact](https://vite.new/preact)  |  [preact-ts](https://vite.new/preact-ts)  |
|     [lit](https://vite.new/lit)     |     [lit-ts](https://vite.new/lit-ts)     |
|  [svelte](https://vite.new/svelte)  |  [svelte-ts](https://vite.new/svelte-ts)  |
|   [solid](https://vite.new/solid)   |   [solid-ts](https://vite.new/solid-ts)   |
|    [qwik](https://vite.new/qwik)    |    [qwik-ts](https://vite.new/qwik-ts)    |

## 最初の Vite プロジェクトを生成する

::: tip 互換性について
Vite は [Node.js](https://nodejs.org/en/) 20.19+, 22.12+ のバージョンが必要です。ただし、一部のテンプレートではそれ以上のバージョンの Node.js を必要としますので、パッケージマネージャーが警告を出した場合はアップグレードしてください。
:::

::: code-group

```bash [npm]
$ npm create vite@latest
```

```bash [Yarn]
$ yarn create vite
```

```bash [pnpm]
$ pnpm create vite
```

```bash [Bun]
$ bun create vite
```

```bash [Deno]
$ deno init --npm vite
```

:::

あとは画面表示に従ってください！

プロジェクト名や使用するテンプレートは、追加のコマンドラインオプションによって直接指定することもできます。例えば Vite + Vue のプロジェクトを生成するには以下のコマンドを実行します:

::: code-group

```bash [npm]
# npm 7+ は追加で 2 つのダッシュが必要:
$ npm create vite@latest my-vue-app -- --template vue
```

```bash [Yarn]
$ yarn create vite my-vue-app --template vue
```

```bash [pnpm]
$ pnpm create vite my-vue-app --template vue
```

```bash [Bun]
$ bun create vite my-vue-app --template vue
```

```bash [Deno]
$ deno init --npm vite my-vue-app --template vue
```

:::

サポートされている各テンプレートの詳細は [create-vite](https://github.com/vitejs/vite/tree/main/packages/create-vite) を参照してください: `vanilla`, `vanilla-ts`, `vue`, `vue-ts`, `react`, `react-ts`, `react-swc`, `react-swc-ts`, `preact`, `preact-ts`, `lit`, `lit-ts`, `svelte`, `svelte-ts`, `solid`, `solid-ts`, `qwik`, `qwik-ts`.

現在のディレクトリーに生成するには、プロジェクト名に `.` を使用します。

## コミュニティーのテンプレート

create-vite はよく使われているフレームワークの基本的なテンプレートを元に、プロジェクトをすばやく開始するためのツールです。他のツールを含んでいたり、別のフレームワークを対象としている、[コミュニティーが管理しているテンプレート](https://github.com/vitejs/awesome-vite#templates)については Awesome Vite をチェックしてみてください。

例えば `https://github.com/user/project` にあるテンプレートについては、`https://github.stackblitz.com/user/project`（プロジェクトの URL の `github` の後に `.stackblitz` を追加）を使ってオンラインで試すことができます。

また、[degit](https://github.com/Rich-Harris/degit) のようなツールを使って、これらのテンプレートからプロジェクトを生成することもできます。プロジェクトが GitHub 上にあり、デフォルトのブランチとして `main` を使用していると仮定すると、次のようにしてローカルコピーを作成できます:

```bash
npx degit user/project#main my-project
cd my-project

npm install
npm run dev
```

## 手動インストール
                 
プロジェクト内に `vite` CLI をインストールするには、次のコマンドを使用します:

::: code-group

```bash [npm]
$ npm install -D vite
```

```bash [Yarn]
$ yarn add -D vite
```

```bash [pnpm]
$ pnpm add -D vite
```

```bash [Bun]
$ bun add -D vite
```

```bash [Deno]
$ deno add -D npm:vite
```

:::

そして、次のような `index.html` ファイルを作成します:

```html
<p>Hello Vite!</p>
```

次に、適切な CLI コマンドをターミナルで実行します:

::: code-group

```bash [npm]
$ npx vite
```

```bash [Yarn]
$ yarn vite
```

```bash [pnpm]
$ pnpm vite
```

```bash [Bun]
$ bunx vite
```

```bash [Deno]
$ deno run -A npm:vite
```

:::

`index.html` は `http://localhost:5173` で配信されます。

## `index.html` とプロジェクトルート {#index-html-and-project-root}

お気づきかもしれませんが、Vite プロジェクトでは `index.html` は `public` 内に隠れているのではなく、最も目立つ場所にあります。これは意図的なものです。開発中、Vite はサーバーで、`index.html` はアプリケーションのエントリーポイントです。

Vite は `index.html` をソースコードとして、またモジュールグラフの一部として扱います。JavaScript のソースコードを参照している `<script type="module" src="...">` を解決します。インラインの `<script type="module">` や `<link href>` で参照される CSS も Vite 固有の機能を利用できます。さらに、`index.html` 内の URL は自動的にリベースされるため、特別な `%PUBLIC_URL%` プレースホルダーは必要ありません。

静的な http サーバーと同様に、Vite には、ファイルの提供元となる「ルートディレクトリー」の概念があります。ドキュメントの残りの部分では `<root>` として示されています。ソースコード内の絶対 URL は、プロジェクトルートをベースとして使って解決されるため、通常の静的ファイルサーバーを使用しているかのようにコードを記述できます（遥かに強力であることを除いては！）。Vite はルート外のファイルシステムの場所に解決される依存関係を処理することもできるため、モノレポベースの構成でも使用できます。

Vite は複数の `.html` エントリーポイントを持つ[マルチページアプリ](./build#multi-page-app)にも対応しています。

#### 代替ルートの指定

`vite` を実行すると、現在の作業ディレクトリーをルートとして使用する開発サーバーが起動します。`vite serve some/sub/dir` で代替ルートを指定できます。
なお、Vite は[設定ファイル（`vite.config.js`）](/config/#configuring-vite)もプロジェクトルート内で解決するので、ルートが変更された場合は設定ファイルも移動する必要があります。

## コマンドラインインターフェイス

Vite がインストールされているプロジェクトでは npm スクリプトで `vite` バイナリーを使用したり、`npx vite` で直接実行できます。生成された Vite プロジェクトのデフォルトの npm スクリプトは次のとおりです:

<!-- prettier-ignore -->
```json [package.json]
{
  "scripts": {
    "dev": "vite", // 開発サーバーを起動。エイリアス: `vite dev`, `vite serve`
    "build": "vite build", // プロダクション用にビルド
    "preview": "vite preview" // プロダクション用ビルドをローカルでプレビュー
  }
}
```

`--port` や `--open` のような追加の CLI オプションを指定できます。すべての CLI オプションのリストは、プロジェクト内で `npx vite --help` を実行してください。

[コマンドラインインターフェイス](./cli.md)について詳しくはこちら。

## 未リリースのコミットの使用

最新機能を試すために新しいリリースが待ちきれない場合は、https://pkg.pr.new を利用すると特定のコミットの Vite をインストールできます:

::: code-group

```bash [npm]
$ npm install -D https://pkg.pr.new/vite@SHA
```

```bash [Yarn]
$ yarn add -D https://pkg.pr.new/vite@SHA
```

```bash [pnpm]
$ pnpm add -D https://pkg.pr.new/vite@SHA
```

```bash [Bun]
$ bun add -D https://pkg.pr.new/vite@SHA
```

:::

`SHA` を任意の [Vite の commit SHA](https://github.com/vitejs/vite/commits/main/) に置き換えてください。古いコミットのリリースは削除されるため、利用できるのは 1 か月以内のコミットだけであることに注意してください。

代わりに、ローカルマシンに [vite repo](https://github.com/vitejs/vite) をクローンしてから自分でビルドとリンクをすることもできます（[pnpm](https://pnpm.io/) が必要）。

```bash
git clone https://github.com/vitejs/vite.git
cd vite
pnpm install
cd packages/vite
pnpm run build
pnpm link --global # このステップでは好きなパッケージマネージャーを使用
```

その後 Vite ベースのプロジェクトに移動し、`pnpm link --global vite`（または、`vite` をグローバルにリンクするために使用したパッケージマネージャー）を実行してください。そして開発サーバーを再起動して最先端の技術に乗っていきましょう！

::: tip Vite を利用している依存関係
依存関係が遷移的に利用している Vite のバージョンを置換するには、[npm overrides](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#overrides) や [pnpm overrides](https://pnpm.io/package_json#pnpmoverrides) を使用する必要があります。
:::

## コミュニティー

質問がある場合やサポートが必要な場合は、[Discord](https://chat.vite.dev) や [GitHub Discussions](https://github.com/vitejs/vite/discussions) でコミュニティーに連絡してください。
