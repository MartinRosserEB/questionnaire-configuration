<script lang="ts">
	import Heading3 from "$lib/components/Heading3.svelte";
	import ResultGraph from "$lib/components/ResultGraph.svelte";
  import Typ_1 from "./enneagramm/Typ_1.svelte";
	import Typ_2 from "./enneagramm/Typ_2.svelte";
	import Typ_3 from "./enneagramm/Typ_3.svelte";
	import Typ_4 from "./enneagramm/Typ_4.svelte";
	import Typ_5 from "./enneagramm/Typ_5.svelte";
	import Typ_6 from "./enneagramm/Typ_6.svelte";
	import Typ_7 from "./enneagramm/Typ_7.svelte";
	import Typ_8 from "./enneagramm/Typ_8.svelte";
	import Typ_9 from "./enneagramm/Typ_9.svelte";
	import type { ResultGraphDataSets } from "$lib/custom-types";

	export let plotData: ResultGraphDataSets;
	export let plotLabels: string[];

  let showMain = true;
  let showWing = false;
  let principalType = plotLabels[plotData[0].data.indexOf(Math.max.apply(Math, plotData[0].data))];
</script>

<Heading3><button on:click={() => { showMain = !showMain}}>Haupttyp</button></Heading3>
{#if showMain}
{#if principalType === 'Typ 1'}
  <Typ_1 />
{:else if principalType === 'Typ 2'}
  <Typ_2 />
{:else if principalType === 'Typ 3'}
  <Typ_3 />
{:else if principalType === 'Typ 4'}
  <Typ_4 />
{:else if principalType === 'Typ 5'}
  <Typ_5 />
{:else if principalType === 'Typ 6'}
  <Typ_6 />
{:else if principalType === 'Typ 7'}
  <Typ_7 />
{:else if principalType === 'Typ 8'}
  <Typ_8 />
{:else if principalType === 'Typ 9'}
  <Typ_9 />
{/if}
{/if}
<Heading3><button on:click={() => { showWing = !showWing}}>Flügel</button></Heading3>
{#if showWing}
{#if principalType === 'Typ 1'}
  <Typ_9 />
  <Typ_2 />
{:else if principalType === 'Typ 2'}
  <Typ_1 />
  <Typ_2 />
{:else if principalType === 'Typ 3'}
  <Typ_2 />
  <Typ_4 />
{:else if principalType === 'Typ 4'}
  <Typ_3 />
  <Typ_5 />
{:else if principalType === 'Typ 5'}
  <Typ_4 />
  <Typ_6 />
{:else if principalType === 'Typ 6'}
  <Typ_5 />
  <Typ_7 />
{:else if principalType === 'Typ 7'}
  <Typ_6 />
  <Typ_8 />
{:else if principalType === 'Typ 8'}
  <Typ_7 />
  <Typ_9 />
{:else if principalType === 'Typ 9'}
  <Typ_8 />
  <Typ_1 />
{/if}
{/if}
<div class="w-full min-h-96">
	<ResultGraph datasets={plotData} labels={plotLabels} />
</div>
