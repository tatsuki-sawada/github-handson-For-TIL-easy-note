from pathlib import Path

# JavaScrptの、new Promise、fetch()then、async awaitの比較

■ 比較対象
1. new Promise()
2. fetch().then()
3. async/await

■ 比較表

| 観点                     | new Promise()                              | fetch().then()                          | async/await                            |
|--------------------------|---------------------------------------------|-----------------------------------------|----------------------------------------|
| ① 主な用途              | 非同期処理のラップ、カスタム制御             | 既存Promiseのシンプル処理               | 可読性・直感的な制御                   |
| ② fetchとの相性         | 原則不要（fetchはPromise返す）               | 相性良し                                 | 相性とても良し                         |
| ③ 可読性・保守性        | 複雑になりやすい                             | ネストが多くなると見づらい               | 同期処理風に書けて◎                   |
| ④ エラーハンドリング    | reject()明示・細かく制御可                   | .catch()で補足                           | try...catch で直感的                   |
| ⑤ 使いどころ            | 自作APIや複雑処理をPromise化                | 軽い処理・流れだけ見たい時               | 実務でよく使う・複雑処理に最適         |

■ 具体例

① new Promise()
```
function customWait(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

② fetch().then()
```
fetch(url)
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

③ async/await
```
async function getData(url) {
  try {
    const res = await fetch(url);
    const data = await res.json();
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}
```

■ 結論
普段は「async/await」推奨。
軽い処理なら「.then()」ですむし、特別な制御が必要なら「new Promise()」を使い分けよう。