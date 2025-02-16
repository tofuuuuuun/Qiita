## 経緯
開発環境でフロント ↔︎ バックエンドで通信する時、`localhost`を直接書いていました。
本番に反映するために毎回書き換えるのは馬鹿らしいので、開発環境、本番環境で動的にURLを切り替えられるようにしました。

設定するときに若干詰まったので、備忘録として残します。

## 環境
- Docker
- Vite
- React
- Typescript

## 設定（失敗）
まずは`.env`を作成して環境変数を定義します。
Reactを使用しているので以下のように設定しました。
```.env
REACT_API_BASE_URL=http://localhost // 開発環境
```

## ログに環境変数を出力
.envの準備ができたので、コンテナを起動してうまく値を持って来れているか確認
```Javascript
console.log( process.env.REACT_API_BASE_URL);

// -> undefined
```

`undefined`が出力されてしまいました…

## 解決
少し調べてみると、Viteを使用しているため、環境変数の定義が間違えていることがわかりました。

```.env
REACT_API_BASE_URL=http://localhost // これはこの環境では間違い

VITE_API_BASE_URL=http://localhost // こちらが正しい
```

環境変数を修正して、再度ログ出力をしてみると
```Javascript
console.log(import.meta.env.REACT_API_BASE_URL);

// -> http://localhost 
```

欲しい値が取れました。
同じように本番環境用の環境変数を定義したファイルを準備して、コンテナ起動時にオーバーライドさせれば、環境を切り替えることができるようになります。

以上です。