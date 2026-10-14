# Homeページ: Newsパネルを右サイドバー→画面下部の固定バーに変更

## Context
現在ホームページ（`home` レイアウト）では、Newsパネルが右カラム（Bootstrapの `col-sm-4`）としてメインコンテンツの右側に表示されている。ユーザーはこれを画面下部に横長の固定バーとして表示し、スクロールしても常に画面に追従する（position: fixed）形に変更したいと考えている。あわせて、右カラムがなくなることで空くスペースはメインコンテンツを画面幅いっぱいに広げて活用する。モバイル表示でもPCと同様に画面下部への固定表示を維持するが、スマートフォンなど狭い画面でバーが縦に膨らんで画面の大半を占有してしまわないよう、バーは常に1行の高さを保ち、記事項目が収まらない場合はその部分だけ横スクロールできるようにする。

## 現状の実装（調査済み）
- `_layouts/homelay.html`: `#homeid`（`col-sm-8`、メインコンテンツ）と `#newsid`（`col-sm-4`、`{% include news.html %}`）が兄弟の列として並び、Bootstrapグリッドの `float: left` で右側に見えている。
- `_includes/news.html`: `.well` の中に `<h4>News</h4>`、`site.data.news` から最大4件の `<p>{{date}}<br>{{headline}}</p>`、最後に「see all News」リンクという縦積みの構造。
- `_layouts/default.html`: `{{ content }}` を `.container-fluid > .row` の中に描画。News/HomeidはこのrowのDOM子要素。
- `css/main.scss`: `#newsid p`、`#newsid img`、`.col-sm-4` のpadding上書きなど、Newsパネル用のスタイルが数箇所に散在。固定ナビバーの既存パターンとして `body { padding-top: 70px; }` があり、`_includes/header.html` の `navbar-fixed-top` と対になっている。今回はこれの「下版」を作る。
- `_includes/footer.html`: ページ最下部の本来のフッター（`.panel > .panel-footer`）。Newsバーをfixedにすると、素のままでは何もしない限りスクロール最下部でこのフッターの上に重なってしまう。今回はこれを防ぎ、**最終的にフッターが常に完全に見える状態にする**（下記「4. フッターが隠れないようにする対策」を参照）。

## 変更方針

### 1. `_layouts/homelay.html`
- `#homeid` のクラスを `col-sm-8` → `col-sm-12` に変更し、メインコンテンツを画面幅いっぱいに広げる。
- `#newsid` のクラス（`col-sm-4`）を削除する（グリッド列として扱う必要がなくなるため）。DOM上の位置はそのままで良い（`#homeid` の直後）。

### 2. `_includes/news.html`
- 横並び表示に適した構造に変更。現在は `<p>{{date}}<br>{{headline}}</p>` で日付と見出しが縦積みになっているが、以下の3ゾーン構成にする:
  1. 左端: `News`（リンクではない、ただの見出しラベル。常に表示・幅は縮まない）
  2. 中央: 各記事の項目（最大4件、1件ずつ `<div class="news-item">日付: 見出し</div>`）を並べた `<div class="news-items">` ラッパー。**このゾーンだけが横スクロール領域になる**（後述）。
  3. 右端: `see all News` リンク（1つだけ、常に表示・幅は縮まない）
  - リンクは末尾の「see all News」の1つのみで、左端に別のリンクが現れるわけではない。
- **スマートフォンなど狭い画面でNewsバーが縦に膨らんで画面の大半を占有してしまわないよう、記事項目は折り返し（wrap）させず、常に1行の高さに固定する。** 項目数が多くて画面幅に収まらない場合は、中央の`news-items`ゾーンだけが横スクロール（スワイプ/トラックパッド）できるようにする。これによりNewsバーの高さは画面幅や記事数によらず常に一定（1行分）になり、左右の「News」ラベルと「see all News」リンクは常に見える位置に固定される。

### 3. `css/main.scss`
- `#newsid` を画面下部に固定表示するスタイルを追加。ポイントは「バー全体は常に1行の高さ」「はみ出す記事項目だけが横スクロール」:
  ```scss
  #newsid {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    z-index: 1030; // navbar-fixed-topと同等
  }
  #newsid .well {
    margin-bottom: 0;
    border-radius: 0;
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 10px 20px;
  }
  #newsid h4 {
    margin: 0;
    flex-shrink: 0; // 左端「News」ラベルは常に全表示、縮まない
    white-space: nowrap;
  }
  #newsid .news-items {
    display: flex;
    align-items: center;
    gap: 20px;
    flex: 1 1 auto;
    min-width: 0; // これがないとflex子要素はoverflowしてくれない
    overflow-x: auto; // 収まらない分はここだけ横スクロール
  }
  #newsid .news-item {
    white-space: nowrap; // 折り返さない → バーの高さが記事数・画面幅に左右されない
    flex-shrink: 0;
  }
  #newsid .news-more {
    flex-shrink: 0; // 右端「see all News」リンクも常に全表示
    margin: 0;
    white-space: nowrap;
  }
  ```
  （モバイル用の個別分岐は設けず、PCと同じ「1行固定＋横スクロール」構成を全幅で維持する。既存の `#newsid p { text-align: left; }` や `#newsid img` のmargin指定は新構造（`p`ではなく`div.news-item`を使う）に合わせて調整・整理する。）

### 4. フッターが隠れないようにする対策
上記3.の設計（記事項目は折り返さず常に1行、はみ出し分は横スクロール）により、Newsバーの高さは記事数や画面幅に左右されず常にほぼ一定になる。とはいえブラウザの文字サイズ設定・ズーム・OSごとのフォント差などで実際の高さが数px前後する可能性はゼロではないため、**固定px値をハードコードするのではなくJSでバーの実高さを測定して本文側の余白に反映する**方式にし、どんな条件でも確実にフッターが完全に見える状態を保証する。
- `_layouts/homelay.html` に小さなインラインスクリプトを追加（既存のjQuery依存なし、素のJSで可）:
  ```html
  <script>
    function adjustNewsBarSpacing() {
      var newsBar = document.getElementById('newsid');
      var homeContent = document.getElementById('homeid');
      if (newsBar && homeContent) {
        homeContent.style.marginBottom = newsBar.offsetHeight + 'px';
      }
    }
    window.addEventListener('load', adjustNewsBarSpacing);
    window.addEventListener('resize', adjustNewsBarSpacing);
  </script>
  ```
  - `load`時とウィンドウの`resize`時にNewsバーの実際の高さを測定し、`#homeid`（＝メインコンテンツ、Newsバーの直前要素）の `margin-bottom` に反映する。これにより、Newsバーの直後にある `.row` / `.container-fluid` の終了タグを経て続く本来のフッターが、常にNewsバー分だけ下に押し出され、重なって隠れることがなくなる。
  - News記事データ（`site.data.news`）はページ読み込み時に確定しておりビルド後に動的変化しないため、`load`と`resize`のタイミングで再計算すれば十分（記事の追加・削除はJekyllの再ビルドを伴うため）。

## 検証方法
- ローカルでJekyllをビルド・起動し（`bundle exec jekyll serve` など、リポジトリの既存の起動手順に従う）、ホームページをブラウザで開いて確認する。
- 確認項目:
  - Newsバーが画面下部に横長で表示され、Newsの見出しが並んでいること。
  - ページをスクロールしてもNewsバーが画面下部に留まり続けること（position: fixed）。
  - メインコンテンツ（挨拶文・カルーセルなど）が画面幅いっぱいに広がっていること。
  - ページ最下部までスクロールした際、本来のフッター内容（Funding/Contact等）がNewsバーに一切隠れず、完全に見える状態であること。ウィンドウ幅を変えてNewsバーの行数（高さ）が変わった場合でも、フッターが隠れないこと（`resize`時の余白再計算が効いているか）。
  - 画面幅を狭めて（スマートフォン相当）表示を確認し、Newsバーが下部に固定されたまま**1行の高さを保ち**、画面の大半を占有しないこと。記事項目が画面幅に収まらない場合は、中央の項目エリアだけが横スクロールでき、左端「News」ラベルと右端「see all News」リンクは常に見えていること。
  - 他ページ（ホーム以外）のレイアウトに影響が出ていないこと。
