<script lang="ts">
	import Scrolly from '$lib/Scrolly.svelte';

	const FlourishID = 3279466;

	const Steps = [
		"En 1950, les émissions mondiales de <mark>CO₂</mark> atteignaient environ 6 milliards de tonnes par an.",
		"Dans les années 1980, ce chiffre avait <mark>triplé</mark>, dépassant les 19 milliards de tonnes annuelles.",
		"Aujourd'hui, nous émettons plus de <mark>36 milliards de tonnes</mark> de CO₂ chaque année.",];
</script>

<div class="article">
	<h2>Un exemple de scrollytelling avec Flourish</h2>
	<p>
		Voici une démonstration simple de la combinaison entre un observateur de défilement en Svelte
		et une story Flourish intégrée. Au fur et à mesure que le lecteur fait défiler les panneaux de
		texte à gauche, la visualisation à droite avance vers la diapositive correspondante.
	</p>
</div>

<Scrolly flourishID={FlourishID} steps={Steps} />

<div class="article">
	<h2>La suite</h2>
	<p>
		L'article continue sous la section interactive. Ce format permet d'alterner entre du contenu
		éditorial classique et des visualisations de données immersives, maintenant l'attention du
		lecteur tout au long du récit.
	</p>
</div>
