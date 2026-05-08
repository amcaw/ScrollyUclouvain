<script lang="ts">
	import Scrolly from '$lib/Scrolly.svelte';

	const FlourishID = 3279466;

	const Steps = [
		"En 1950, les émissions mondiales de <mark>CO₂</mark> atteignaient environ 6 milliards de tonnes par an.",
		"Dans les années 1980, ce chiffre avait <span style='background-color: red; color: white; font-weight: bold; border-radius: 4px; padding: 0 0.25em;'>triplé</span>, dépassant les 19 milliards de tonnes annuelles.",
		"Aujourd'hui, nous émettons plus de <mark>36 milliards de tonnes</mark> de CO₂ chaque année.",];
</script>

<div class="article">
	<h1>Ceci est le titre principal de l'article</h1>
	<p class="byline">
		Par <strong>John Doe</strong>, <strong>Jane Doe</strong> et <strong>Michel Doe</strong>
		<span class="byline-sep">—</span>
		<time datetime="2026-05-07">7 mai 2026</time>
	</p>
	<p class="intro">
		Ceci est le chapeau avec du texte lorem ipsum. Lorem ipsum dolor sit amet, consectetur
		adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
		minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
	</p>
</div>

<Scrolly flourishID={FlourishID} steps={Steps} />

<div class="article">
	<h2>La suite</h2>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut
		labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
		laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in
		voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
		non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
	</p>

	<figure>
		<img src="/burger_2.png" alt="Illustration d'un burger" />
		<figcaption>Légende de l'image : un délicieux burger en illustration.</figcaption>
	</figure>

	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut
		labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
		laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in
		voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
		non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
	</p>
</div>

<div class="methodology">
	<h3>Comment avons-nous travaillé ?</h3>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt
		ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation
		ullamco laboris nisi ut aliquip ex ea commodo consequat.
	</p>
	<p>
		<a href="/methodologie">Retrouvez notre méthodologie complète en cliquant ici</a>
	</p>
</div>

<div class="credits">
	<p>
		Un article de <strong>John Doe</strong>, <strong>Jane Doe</strong> et
		<strong>Michel Doe</strong>.
	</p>
</div>
