## 経緯
これまでimport文を相対パスで記述していました。
```
import { Modal } from '../../../Components/Modal';
```

フォルダ階層が浅い時にはまだいいのですが、階層が深くなるにつれてどこを見に行っているのかわからなくなり、ぱっと見の見通しがかなり悪くなっていました。

ということでimport文を絶対パスで記述するように設定しました。

## 環境
- React
- Typescript
- Vite

## 設定内容
tsconfig.json、tsconfig.app.json、vite.config.tsに設定追加していきます。

tsconfig.jsonにbaseurlとpathsを追加します。
baseurlはTypescriptのモジュール解決の基準になるディレクトリを設定します。
pathsも一緒に記述します。
今回は"@"起点で絶対パスを記述できるようにしたかったので以下のような設定にしています。
```
 "compilerOptions": {
    "baseUrl": ".",         // ←追加
    "paths": {              // ←追加
      "@/*": ["./src/*"]    // ←追加
    }
  }

// tsconfig.app.jsonにも同じ設定をする

```

tsconfig.app.jsonにも同じように設定を追加しないとエラーになってしまったので、こちらにも同様の
設定を追加しておきます。

次にvite.config.tsにも設定を追記します。
resolve.aliasを追加します。
こちらにも設定を追記しないとビルド、実行時にエラーになります。

```
export default defineConfig({
  root: './',
  publicDir: "public",
  plugins: [tsconfigPaths(), react()],
  resolve: {        // ←追加
    alias: {        // ←追加
      "@": "/src",  // ←追加
    }
  }
  })
```


設定終わったら各ファイルのimport文を直しましょう。
```
import { Modal } from '@/components/Modal/Modal';
```

以上です。
