<script lang="ts">
	import Paragraph from "$lib/components/Paragraph.svelte";
	import UnorderedList from "$lib/components/UnorderedList.svelte";
	import ResultGraph from "$lib/components/ResultGraph.svelte";
	import type { ResultGraphDataSets } from "$lib/custom-types";

	export let plotData: ResultGraphDataSets;
	export let plotLabels: string[];
</script>

<Paragraph>Die Transaktionsanalyse kennt 5 Innere Antreiber:</Paragraph>
<UnorderedList>
  <li>Sei perfekt!</li>
  <li>Sei gefällig!</li>
  <li>Streng Dich an!</li>
  <li>Sei stark!</li>
  <li>Beeil Dich!</li>
</UnorderedList>
<Paragraph>Im Grunde genommen repräsentieren die inneren Antreiber positive Eigenschaften wie:</Paragraph>
<UnorderedList>
  <li>Genauigkeit und Fehlerlosigkeit (Sei perfekt!)</li>
  <li>Freundlichkeit und Liebenswürdigkeit (Sei anderen gefällig!)</li>
  <li>Gründlichkeit und Durchhaltevermögen (Streng Dich an!)</li>
  <li>Stärke und Unabhängigkeit (Sei stark!)</li>
  <li>Schnelligkeit und die Fähigkeit, Chancen zu nutzen (Beeil dich!)</li>
</UnorderedList>
<Paragraph>Das Konzept der inneren Antreiber beschreibt ein übertriebenes, gelegentlich unpassendes Ausleben dieser Eigenschaften. Menschen unter Antreiber können nicht mehr wählen, ob sie beispielsweise etwas perfekt machen oder ob sie freundlich sein wollen. Sie werden von ihrem Antreiber dazu gezwungen.</Paragraph>
<Paragraph>Ihnen zu folgen kann Zeit und Kraft kosten. Ihnen nicht zu folgen führt zunächst zu schlechten Gefühlen, wie dass man sich nicht gut genug fühlt.</Paragraph>
<div class="w-full min-h-96">
	<ResultGraph datasets={plotData} labels={plotLabels} />
</div>
