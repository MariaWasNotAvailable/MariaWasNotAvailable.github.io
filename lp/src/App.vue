<template lang="html">
	<main>
		<header id="header">
			<div class="header flexwrap">
				<h1>This is an example landing page</h1>
				<p>Made with love using Vue + Vite</p>
				<a href="#" class="button">Call to action</a>
			</div>
		</header>
		<section class="wrapper">
			<div class="inner">
				<h2>Copy</h2>
				<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
				</br><span class="light">Praesent tristique magna sit amet purus. Malesuada fames ac turpis egestas integer eget aliquet nibh praesent. 
					Egestas tellus rutrum tellus pellentesque eu tincidunt tortor. Magna fermentum iaculis eu non diam phasellus vestibulum. 
					Lacus vel facilisis volutpat est velit egestas dui id ornare. Augue neque gravida in fermentum. 
					Fringilla urna porttitor rhoncus dolor purus non enim praesent. Mi sit amet mauris commodo quis imperdiet massa. 
					Proin nibh nisl condimentum id venenatis a. </span>
			</div>
		</section>

		<section class="wrapper">
			<div class="inner">
				<h2>Hero</h2>
					<div id="hero-content">
						<ol>
							<li>Lorem</li>
							<li>Ipsum</li>
							<li>Et cetera</li>
						</ol>
						<img id="hero-image" src="./assets/hero.webp" loading="lazy"/>
					</div>
			</div>
		</section>

		<section class="wrapper">
			<div class="inner">
				<h2>Tabs</h2>
				<div>
					<TabsWrapper>
						<tab title="Pie chart" class="flex">
							<div class="pie-flex">
								<div class="pie-chart" :style="{ backgroundImage: blue_angle }" :title=pie_label></div>
								<div>
									<a class="pie-button orange" @click.self=postOrange()>Orange</a>
									<a class="pie-button blue" @click.self=postBlue()>Blue</a>
								</div>
							</div>
							<div>
								<p>Sample results of a poll.</p>
								<p>The buttons are a mock-up because the (not mine) API endpoint hates me currently. Oops!</p>
							</div>
						</tab>
						<tab title="Text content" class="flex">
							<img src="./assets/laptop.webp" loading="lazy"/>
							<div>
								<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
								<span class="light">Praesent tristique magna sit amet purus. Malesuada fames ac turpis egestas integer eget aliquet nibh praesent. 
									Egestas tellus rutrum tellus pellentesque eu tincidunt tortor. Magna fermentum iaculis eu non diam phasellus vestibulum. 
									Lacus vel facilisis volutpat est velit egestas dui id ornare. Augue neque gravida in fermentum. 
									Fringilla urna porttitor rhoncus dolor purus non enim praesent. Mi sit amet mauris commodo quis imperdiet massa. 
									Proin nibh nisl condimentum id venenatis a.
								</span>
							</div>
						</tab>
						<tab title="More text">
							<span class="light">Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
								Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
								Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
								Faucibus purus in massa tempor nec feugiat. Venenatis tellus in metus vulputate eu. Ante metus dictum at tempor commodo. 
								Viverra ipsum nunc aliquet bibendum enim facilisis gravida neque convallis. Ornare arcu odio ut sem nulla pharetra diam. 
							</span>
						</tab>
					</TabsWrapper>
				</div>
			</div>
		</section>

		<footer id="footer">
			<div id="footer-links">
				<a href="#" class="light">Facebook</a>
				<a href="#" class="light">X</a>
				<a href="#" class="light">Instagram</a>
				<a href="#" class="light">Contact us</a>
			</div>

			<p class="copyright">&copy; Maria 2024</p>
		</footer>
	</main>
</template>

<script setup lang="ts">
import Tab from './components/Tab.vue'
import TabsWrapper from './components/TabsWrapper.vue'

const api_url = "";
const api_key = ""; // dotenv recommended
let colors = {blue: "3", orange: "5"};

/*try {
	colors = await fetch(api_url, { method: "GET", headers: { "Content-Type": "application/json", "x-apikey": api_key, "cache-control": "no-cache" } })
		.then((response) => response.json());
} catch (err) {
	console.log(`Error connecting to restdb.io API: ${err}`)
}*/

const blue_angle = `conic-gradient(cornflowerblue 0 ${parseInt(colors["blue"]) / (parseInt(colors["blue"]) + parseInt(colors["orange"]))}turn, orange 0)`;
const pie_label = `${colors["blue"]}/${colors["orange"]}`;

async function post(color:string) {
	let new_color_val = String(parseInt(colors["blue"]) + 1);

	await fetch(api_url, {
		method: "PUT",
		headers: {
			"Content-Type": "application/json",
			"x-apikey": api_key,
			"cache-control": "no-cache"
		},
		body: JSON.stringify({[color]: [new_color_val]})
	});
};

async function postOrange() {
	//await post("orange");
};

async function postBlue() {
	//await post("blue");
};

defineExpose({
	postOrange,
	postBlue
});

</script>

<style scoped lang="css">
#hero-content {
	display: flex;
    justify-content: space-around;
    background: linear-gradient(105deg, #003E80 40%,  white 40.2%);
	font-size: 2em;
	line-height: 1.5em;
}

#hero-content > ol {
	color: white
}

.pie-chart {
	width: 12em;
	height: 12em;
	border-radius: 50%;
	background-image: conic-gradient(cornflowerblue 0 180deg, orange 0);
	filter: saturate(40%) brightness(120%);
	transition: filter 0.3s ease-in-out;
}

.pie-chart:hover {
	filter: saturate(100%) brightness(100%);
}

.pie-button {
	min-width: 4em;
	transition: 
		color 0.3s ease-in-out, 
		border-bottom-color 0.3s ease-in-out,
		background-color 0.3s ease-in-out,
		background-size 0.5s ease-in-out;
	background-image: linear-gradient(90deg, rgba(224, 224, 224, 25%), rgba(255, 255, 255, 25%));
	background-size: 0% 100%;
	background-repeat: no-repeat;
	background-position: left 100%;
	background-color: #f5f5f5;
	padding: 0.4em 0.6em;
	margin: 1.5em 0.25em;
	border-radius: 10px;
	border: solid #c1d7ee;
	border-width: 2px;
	cursor: pointer;
	display: inline-block;
	line-height: 1.5em;
	text-align: center;
	text-decoration: none;
	margin-bottom: 0.75em;
	color: #00102A !important;
}

.pie-button:hover {
	background-size: 100% 100%;
}

.pie-flex {
	display: flex;
	flex-direction: column;
	align-items: center;
	gap: 0.5em;
}

.orange:hover {
	background-color: orange;
}

.blue:hover {
	background-color: cornflowerblue;
}

</style>
