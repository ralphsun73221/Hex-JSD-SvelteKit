<script lang="ts">
	let hA = 0;
	let mA = 0;
	let sA = 0;

	// let time = new Date(); // 獲取當下時間

	// 將當下時間設定成變數
	// let hour: number = time.getHours();
	// let minute: number = time.getMinutes();
	// let second: number = time.getSeconds();

	// console.log(`${hour}:${minute}:${second}`);

	function getTimes() {
		// 取得當下時間，並將時間使用 object return
		let time = new Date();
		let hour: number = time.getHours();
		let minute: number = time.getMinutes();
		let second: number = time.getSeconds();

		return { h: hour, m: minute, s: second };

		// console.log(`${hour}:${minute}:${second}`);
	}

	function position() {
		// 用來計算指針位置，最後 return 計算後的數值
		// 目前可以知道的是每 5 rotate = 1 秒鐘
		const { h, m, s } = getTimes();

		let secondAngle = s * 6;
		let minuteAngle = m * 6 + (s / 60) * 6;
		let hourAngle = (h % 12) * 30 + (m / 60) * 30 + (s / 3600) * 30;

		sA = secondAngle;
		mA = minuteAngle;
		hA = hourAngle;

		// return { sA: secondAngle, mA: minuteAngle, hA: hourAngle };
		// console.log(`${hourAngle}:${minuteAngle}:${secondAngle}`);
	}

	// setInterval(getTimes, 1000); // 每 1000 毫秒（1秒鐘）執行一次 getTime 取得當下時間
	setInterval(position, 1000);
</script>

<svelte:head>
	<link
		rel="icon"
		href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🕒</text></svg>"
	/>
	<title>時鐘</title>
</svelte:head>

<main>
	<div class="clock-bg">
		<div class="second" style="transform: rotate({sA}deg);"></div>
		<div class="hour" style="transform: rotate({hA}deg);"></div>
		<div class="minute" style="transform: rotate({mA}deg);"></div>
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
			// display: flex;
			// justify-content: center;
			// align-items: center;
			position: relative;

			.hour,
			.minute,
			.second {
				position: absolute;
				left: 50%;
				bottom: 50%;
				transform-origin: bottom;
				transform: translate(-50%, -100%);
			}

			.hour {
				width: 8px;
				height: 72px;
				background-image: url('/hour-hand.svg');
				// background-color: $hour;
				// border-radius: 8px 8px 0 0;
				// display: flex;
				// justify-content: center;
				// align-items: flex-end;
				// transform: rotate(250deg);
			}

			.minute {
				width: 8px;
				height: 96px;
				background-image: url('/minute-hand.svg');
				// background-color: $minute;
				// border-radius: 8px 8px 0 0;
				// position: absolute;
				// display: flex;
				// justify-content: center;
				// align-items: flex-end;
				// transform: rotate(170deg);
			}

			.second {
				width: 13px;
				height: 120px;
				background-image: url('/second-hand.svg');
				// background-color: $seconds;
				// border-radius: 8px 8px 0 0;
				// position: absolute;
				// display: flex;
				// justify-content: center;
				// align-items: flex-end;
				// transform: rotate(90deg);
			}
		}

		.clock-bg::before {
			content: '';
			position: absolute;
			left: 50.5%;
			bottom: 46.5%;
			transform-origin: bottom;
			transform: translate(-50%, -100%);
			width: 14px;
			height: 14px;
			border-radius: 50%;
			background-color: $hour;
			z-index: 1;
		}
	}
</style>
