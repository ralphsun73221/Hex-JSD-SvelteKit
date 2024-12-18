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
		<div class="second"><i></i></div>
		<div class="hour"><i></i></div>
		<div class="minute"><i></i></div>
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
			display: flex;
			justify-content: center;
			align-items: center;
      position: relative;

			.hour {
				position: absolute;
				display: flex;
				justify-content: center;
				align-items: flex-end;
				transform: rotate(200deg);
				i {
					position: absolute;
					width: 8px;
					height: 72px;
					background-image: url('/hour-hand.svg');
				}
			}

			.minute {
				position: absolute;
				display: flex;
				justify-content: center;
				align-items: flex-end;
				transform: rotate(134deg);
				i {
					position: absolute;
					width: 8px;
					height: 96px;
					background-image: url('/minute-hand.svg');
				}
			}

			.second {
				position: absolute;
				display: flex;
				justify-content: center;
				align-items: flex-end;
				transform: rotate(157deg);
				i {
					position: absolute;
					width: 12px;
					height: 126px;
					background-image: url('/second-hand.svg');
				}
			}
		}
		.clock-bg::before {
			content: '';
			position: absolute;
			width: 8px;
			height: 8px;
			border-radius: 50%;
			background-color: #fff;
			// z-index: 2;
		}
	}
</style>
