<script lang="ts">
	let time = new Date(); // 獲取當下時間

	// 將當下時間設定成變數
	let hour = time.getHours();
	let minute = time.getMinutes();
	let second = time.getSeconds();

	console.log(`${hour}:${minute}:${second}`);
</script>

<svelte:head>
	<link
		rel="icon"
		href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>s🕒</text></svg>"
	/>
	<title>時鐘</title>
</svelte:head>

<main>
	<div class="clock-bg">
		<div class="hour"></div>
		<div class="minute"></div>
		<div class="second"></div>
	</div>
</main>

<style lang="scss">
	$main-color: #293b29;
	$senderay-color: #435947;
	$hour: #ee7e31;
	$minute: #ffffff;
	$seconds: #c1fd50;

	main {
		width: 1200px;
		height: 800px;
		margin: 0 auto;
		align-content: center;
		background-color: $main-color;
		color: $minute;

		.clock-bg {
			width: 500px;
			height: 500px;
			background-image: url('/clock-bg.svg');
			margin: 0 auto;
			position: relative;

			.hour {
				width: 72px;
				height: 8px;
				background-image: url('/hour-hand.svg');
				position: absolute;
				top: 48.6%;
				left: 49.3%;
			}

			.minute {
				width: 8px;
				height: 96px;
				background-image: url('/minute-hand.svg');
				position: absolute;
				top: 31%;
				left: 49.2%;
			}

			.second {
				width: 12px;
				height: 126px;
				background-image: url('/second-hand.svg');
				position: absolute;
				top: 50%;
				left: 48.7%;
			}
		}
	}
</style>
