<script>
  // 定義一串數字陣列
  let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

  // 將 card-content 裡面會使用到的資料統一用函式處理
  const CARD_CONTENT = (num) => {
    console.log('目前的 num:', num); // 會看到是 2,3,4...9
    console.log('完整的 arr:', arr); // 會看到是 [1,2,3,4,5,6,7,8,9]
    return arr.map((item) => `${num} X ${item} = ${num * item}`);
  };
</script>

<svelte:head>
  <link
    rel="icon"
    href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🧮</text></svg>"
  />
  <title>九九乘法表</title>
</svelte:head>

<main>
  <div class="title">
    <div class="line">
      <span class="corner x-left">x</span>
      <span class="line-content"></span>
      <span class="corner x-left">x</span>
    </div>
    <div class="title-content">
      <h1>九九乘法表</h1>
      <h2>MULTIPLICATION CHART</h2>
    </div>
    <div class="line">
      <span class="corner x-left">x</span>
      <span class="line-content"></span>
      <span class="corner x-left">x</span>
    </div>
  </div>
  {#each arr.slice(1) as num}
    <div class="card-bcg">
      <div class="card-body">
        <p class="card-title">{num}</p>
        {#each CARD_CONTENT(num) as content}
          <p class="card-content">{content}</p>
        {/each}
      </div>
    </div>
  {/each}
</main>
<footer>
  <p>Copyright © 2024 HexSchool. All rights reserved.</p>
</footer>

<style lang="scss">
  $main-color: #2eb738;
  $bgc: #f0f0f0;
  $card-color: #ffffff;
  $card-bgc: #d8d8d8;

  main {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    margin: 0 auto;
    padding: 80px 85px 80px 85px;
    max-width: 1280px;
    max-height: 1372px;
    background-color: $bgc;

    .title {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      height: 100%;
      color: $main-color;

      h1 {
        font-size: 56px;
      }
      h2 {
        font-size: 24px;
      }

      .line {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 100%;

        .corner {
          color: $main-color;
          font-size: 24px;
        }

        .line-content {
          flex-grow: 1;
          height: 1px;
          margin: 0 20px;
          margin-top: 5px;
          background-color: $main-color;
        }
      }
    }

    .card-bcg {
      height: 100%;
      background-color: $card-color;
      box-shadow: 0px 3px 10px #d8d8d8;
      border-radius: 100px 0px 30px 0px;
      color: $main-color;

      .card-body {
        display: inline-flex;
        flex-direction: column;
        flex-wrap: wrap;
        justify-content: space-between;
        align-content: center;
        padding: 52px 40px;
        width: 100%;
        height: 366px;

        .card-title {
          display: inline;
          height: 153px;
          font-size: 128px;
          text-align: center;
          text-shadow: 4px 3px 0px #f0f0f0;
          line-height: 1.1;
        }

        .card-content {
          margin: 0 15px;
          font-size: 24px;
          letter-spacing: 1px;
        }
      }
    }
  }

  footer {
    max-width: 1280px;
    margin: 0 auto;
    padding: 5px 0;
    padding-right: 85px;
    background-color: $main-color;
    text-align: end;
    color: $card-color;
  }
</style>
