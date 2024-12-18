# JavaScript 題目篇 - 新手 JS 地下城（但是用 Svelte 來做)

## Journal

- 想要熟練的唯一方法，就是大量的練習。
- 所以這個地方就用來紀錄練習以及解題的過程，讓自己可以累積更多的經驗
- 這次使用之前一直想嘗試的新東西，譬如使用 `display:grid` 來當成主要的排版方式，以及使用 SCSS 來撰寫 style，然後使用 vite 當成打包工具

### 241208

- HTML 以及 CSS 都跟原本的架構相同，只不過改用 Svelte 來實作
- `{#each}` 的邏輯完成，但是現在卡在要如何讓樣式跟設計稿一樣
- 試了不少的方式，最終還是用 `display: flex` 做出來差不多的效果，但是還有地方需要微調，但大的架構應該不會再有什麼很大的變動
- 結果還是用了一個最簡單的 `space-between` 就解決了排版問題

### 241209 - 九九乘法表的邏輯是什麼？

- 這個可以好好的紀錄一下，為何程式碼最終會是現在這個樣子
- 首先重構做了這幾件事情：
  1. 一個是將原本重複 9 次的 `card-body` 縮減到一次，
  2. 原本的 card-title 使用 `arr.slice(1)` 來產生，`slice()` 的用途是**指定陣列裡面開始處理的位置**，由於裡面寫了 1，所以會從 2 開始處理（因為 0 被跳過）
  3. 增加一個**函式表達式**用來產生 `card-content` 的內容，
  4. 2 跟 3 都搭配 `{#each}` 來產生出重複使用的內容
- 我也是後來才發現原來 `{#each}` 裡面還可以再包 `{#each}`

### 241210

- 終於完成了第一個卡片的裝飾
- 本來的想法是用 `board` 來做，但是沒有辦法只出現上下，所以作罷
- 還是用純手工來做，之前是我想太多了...
- 順便用了之前看到的[使用 emoji 來當網站 Favicon](https://css-tricks.com/emoji-as-a-favicon/)
- Main 改成了 Nav，首頁就是九九乘法表

#### 關於 route

- 想把首頁改成完成的列表，所以會處理到 route 的東西，所以來記錄一下截止目前為止 Svelte 的 route 要如何設定
- 目前 Svelte 沒有內建 route 管理，但是 SvelteKit 裡面有（使用 `+page`)
- 如果不用 SvelteKit 的話，那就要使用 [svelte-routing](https://github.com/jpcutshall/svelte5-router) 這個套件來處理
- 當然用純的也可以，只是需要做的前置作業就會比較多一點
  - 建立要使用的 `.html` 檔案，譬如要連結到 `A.html` 就建立一個對應的，放的位置無所謂，但我自己會放到 pages
  - 在 `A.html` 裡面加入要使用的 Svelte component
  - 在 `index.html` 裡面建立 `<a>` 到 `A.html`
  - main.js 也會需要做對應的修改，比較簡單的方式是將會使用的到的 component 都 import 到這個檔案，然後根據不同的頁面寫不同的參數
  - 或是用一個簡單的判斷也可以
  - 不過後來想想，比較符合 Svelte 的做法應該是寫一個 component，放入 index.html 裡面的內容，然後用這個 component 來處理
- 後來選擇的處理方式比較土炮一點，就是不同的 html 搭配一個 js，可能之後會再用 SvelteKit 設定 route，但現在就先不花太多時間在這個上面了
- 因為是當時想的方法行不通，主要是 Svelte 的架構，由於一個 html 一定會使用一個 js 來引入，所以如果有第二個 html 就一定需要一個對應的 js，除非是使用套件或是改用 SvelteKit，不然這應該是目前唯一解

### 241213 - 時鐘

- `Nav.svelte` 那邊之前一直會出現網址重複的情況，預設的 `index.html` 是九九乘法，第一次點擊到時鐘沒有問題，但是當再次點擊九九乘法表的時候網址就會出現問題
- 後來發現是我其實可以不用在 `Nav` 裡面去指定絕對路徑（`<a href="./src/pages/01.html>`），可能是因為其實這兩頁都在同一個資料夾底下，多加前面那一個 . 反而會讓路徑指到錯誤的地方去
- 這個問題不大就是了，但沒有用 route 的話就是會需要多一點時間來排除
- 原本想說自己來刻那個時鐘，但是我發現裡面那個刻度有點太難了，偷吃步用圖片好了
- 不過寫好的 code 就不刪掉了

### 241216 - SvelteKit

- 上個星期在處理完樣式推送 Clock 的時候發現一個情況，就是點擊 `Nav` 的時鐘頁面後還是出現九九乘法表，我猜測可能是 Compile 時並不會分開去處理不同頁面的 JS，而是統一由單一的 JS 檔案來處理（也就是 `index.html` 裡面載入的那一支），由於我使用的方式並不是官方建議的做法（因為官方建議用 SvelteKit），所以才會導致無論如何都只會吐九九乘法表的內容
- 看起來最終還是要用 SvelteKit 來處理 route，所以之後的開發會從這邊繼續
- SvelteKit 的架構跟原生的有許多的不同，最明顯的一點就是沒有 `index.html` 這個檔案，取而代之的是 `app.html`，原本的 src 除了 `lib` 之外，多了 `server` `routes` `params` 跟其他可選檔案，但裡面除了 `app.html` 跟 `src/routes` 之外，其他都不是必須的
- 由於這次主要想用的是路由這個功能，就先紀錄這個部分的重點
- route 的檔案開頭都是由 `+` 為第一個，並且使用資料夾為進入點，如果我建立了一個 `src/routes/about`，那對應的就是 `https://www.something.com/about` 這個 rotues
- 前面提到 `src/routes` 裡面的檔案都是用 `+` 開頭，但也不是 `+` 之後可以亂取，目前定義的總共有四種，分別是：
  1. +page
     - 可以把這個視為該 routes 的 index.html，預設的情況下這個頁面算繪的模式是 SSR，也就是伺服器算繪
     - 並且可以透過 `data` prop 從 `load` function 接受資料
  2. +layout
     - 這個東西的邏輯有點類似於 Astro 裡面的 layout，也就是那些可以重複使用的 component，譬如 Nav、Footer 這種
     - 最重要的就是必須要加入 `{@render}` 這個標籤，這樣他才會去算繪其他引入的 component
     - 原先在 Svelte 4 的時候是使用 <slot /> 雖然現在還是可以用，但是畢竟官方已經將這個功能列為過時，之後也會拔掉，所以還是用 `{@render}` 比較一勞永逸
  3. +error
     - 這個目前應該遇不到，之後有遇到再說
  4. +server
     - 這個目前應該遇不到，之後有遇到再說

### 241217

- 今天把原本的 component 都轉移到了這邊，有些東西值得紀錄一下
  - 首先就是 `+layout.svelte` 裡面的 `let { children } = $props();`，我後來發現這個東西的目的是為了告訴 Svelte 可以在這個地方去算繪 `{@render children()}` 其他的 `+page` 的內容，children 是 Svelte 內建的一個[函式](https://svelte.dev/docs/svelte/@render#Optional-snippets)
  - 雖然 Svelte 5 可以直接轉換大部份的 TS，但是他也不是全部都可以正常認得（因為 ESlint 可能會報類似 `eslint: Parsing error: Unexpected token :` 這種的錯誤，但你明明沒有寫錯），官方的建議是[安裝另外一個外掛](https://svelte.dev/docs/kit/integrations)然後去 `svelte.config.js` 裡面設定，而且 SCSS 跟 SASS 也都需要做這個動作之後才能正常被認識（其實就是交給 vite 來處理啦）
    - 結果還是一直出現...算了之後有時間再來研究好了
  - 我一開始不懂 `app.html` 裡面的 `%sveltekit.head%` 可以幹嗎（只知道是用來佔位的），後來發現他是用來接受 component 裡面 `<title></title>` 跟 `<link></link>` 的，這樣就可以顯示每一頁不同的網頁標題，以及根據不同的 component 的需求載入不同的其他的 JS
    - 使用的方式是在對應的 component 裡面加上 `<svelte:head>內容</svelte:head>`，這樣在裡面的內容就會自己加到 `<head>` 裡面 
- 我現在的問題就是為何 `static/clock-bg.svg` 沒有辦法顯示，明明其他的 svg 都沒有問題啊...
  - 好的，因為我的路徑寫錯了，SvelteKit 會自動的去 `/static` 裡面找對應的資源，所以在沒有其他子資料夾的情況下只要直接 `/檔案名稱` 就可以了

### 241218

- 意外的是，如果使用 VScode 的話同樣的錯誤（`eslint: Parsing error: Unexpected token :`）不會出現...，算了這個也不是重點，只是覺得有點莞爾