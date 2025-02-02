## 経緯
react　routerを使用してコンポーネントを切り替えるようにしたくて以下のような実装をしていました。

```typescript
<main>
<BrowserRouter>
    <Routes>
    <Route path='/pageA' element={<A />} />
    <Route path='/movie' element={<B />} />
    </Routes>
</BrowserRouter>
</main >
```

しかしこの状態では、いざ画面を表示してみるとエラーがdevツールに出力されており、何も表示されません。
```
TypeError: Cannot destructure property 'basename' of 'm.useContext(...)' as it is null.
```

## 解決
少し調べてみると`BrowserRouter`はアプリケーション全体をラップするようにしないといけないようです。
`main.tsx`で`App.tsx`を`BrowserRouter`でラップするようにすると・・・

```typescript
<BrowserRouter>
    <App />
</BrowserRouter>
```

```typescript
<main>
    <Routes>
    <Route path='/pageA' element={<A />} />
    <Route path='/movie' element={<B />} />
    </Routes>
</main >
```

うまく画面表示されました。

