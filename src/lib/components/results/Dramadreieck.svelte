<script lang="ts">
	import Paragraph from "$lib/components/Paragraph.svelte";
	import Heading3 from "$lib/components/Heading3.svelte";
	import ResultGraph from "$lib/components/ResultGraph.svelte";
	import type { ResultGraphDataSets } from "$lib/custom-types";

	export let plotData: ResultGraphDataSets;
	export let plotLabels: string[];
	let opfer: number = 15, verfolger: number = 15, retter: number = 15;

	$: {
		if (plotData.length > 0) {
			verfolger = plotData[0].data[plotLabels.findIndex(pl => pl === 'Verfolger-Rolle')];
			opfer = plotData[0].data[plotLabels.findIndex(pl => pl === 'Opfer-Rolle')];
			retter = plotData[0].data[plotLabels.findIndex(pl => pl === 'Retter-Rolle')];
		}
	}	
</script>

<Paragraph>Das Drama-Dreieck hilft dir, die Entstehung und den Hergang von Konflikten besser zu verstehen. Es lässt sich auf alle zwischenmenschlichen Beziehungen anwenden: mit Vorgesetzten, Kollegen, in der Partnerschaft, mit Freunden oder mit Familienangehörigen.</Paragraph>
<Paragraph>Das Drama-Dreieck beschreibt drei Rollen. Wenn Menschen sie einnehmen, kann das zu unheilvollen Verstrickungen führen. Die drei Rollen werden nachfolgend erklärt.</Paragraph>
<div id="svg-container" class="w-full h-72 mt-10 mb-3">
	<svg class="w-full h-full" viewBox="0 0 200 200" preserveAspectRatio="xMidYMid" xmlns="http://www.w3.org/2000/svg">
	  <polygon points="20,35 180,35 90,150" class="stroke-slate-500 stroke-1" fill-opacity="0" />
	  <circle r="{verfolger}" cx="20" cy="35" class="fill-red-400" />
	  <text x="0" y="10" class="fill-black text-sm">Verfolger-Rolle</text>
	  <circle r="{retter}" cx="180" cy="35" class="fill-blue-400" />
	  <text x="140" y="10" class="fill-black text-sm">Retter-Rolle</text>
	  <circle r="{opfer}" cx="90" cy="150" class="fill-yellow-500" />
	  <text x="50" y="185" class="fill-black text-sm">Opfer-Rolle</text>
	   Sorry, your browser does not support inline SVG.
	</svg> 
</div>
<Heading3>Die Retter-Rolle</Heading3>
<Paragraph>Menschen, die häufig die Retter-Position besetzen, werden von der Gesellschaft im Allgemeinen als großzügig und hilfsbereit wahrgenommen. Doch sie haben auch die Neigung, andere in ihrer Fähigkeit selbst nachzudenken und selbstverantwortlich zu handeln, unbewusst abzuwerten.</Paragraph>
<Paragraph>Ihre grundsätzliche und unreflektierte Idee, wie man mit anderen in Beziehung kommt, besteht darin geben zu müssen. Nur wenn sie mehr geben als nehmen, glauben sie in einer Beziehung sicher verbunden zu sein (Bernd Taglieber). Sie tun dies aus einer fürsorglichen Elternhaltung heraus. Damit werden die Beziehungspartner tendenziell zu Kindern.</Paragraph>
<Heading3>Die Verfolger-Rolle</Heading3>
<Paragraph>Menschen, deren Lieblingsrolle im Drama-Dreieck die Verfolger-Position ist, werden häufig als dogmatisch, selbstgewiss oder streng wahrgenommen.</Paragraph>
<Paragraph>Sie verstehen es, andere in die Defensive einzuladen. Ihnen ist es wichtig, sich überlegen zu fühlen. Sie wissen genau, was richtig und was falsch ist, und denken stark in schwarz-weiß Kategorien. Sie treten oft wie überkritische Eltern oder Lehrer auf.</Paragraph>
<Paragraph>Personen aus der Verfolger-Position werten andere häufig ab. Verfolger besetzen die Position: „Ich bin in Ordnung, die anderen sind nicht in Ordnung, ich muss sie darauf hinweisen.“, so wie es auch die Retter tun. Allerdings sind sie nicht fürsorglich unterwegs, sondern streng und kritisch.</Paragraph>
<Heading3>Die Opfer-Rolle</Heading3>
<Paragraph>Menschen, die die Opfer-Rolle besetzen, präsentieren sich anderen gegenüber häufig als schwach und hilflos. Diese Personen werten sich selbst, ihre Fähigkeit zu denken und die Verantwortung für ihr eigenes Handeln zu übernehmen, ab. Sie zeigen nach außen oft ein schwaches Selbstbewusstsein. Manche zeigen auch nur in bestimmten Situationen verstärkt Hilfsbedürftigkeit.</Paragraph>
<Paragraph>Opfer im Sinne des Drama-Dreiecks tragen zu ihrer eigenen Situation selbst mit bei. Sie unternehmen auch keine Anstrengung aus ihr herauszukommen und laden andere zu Rettungsaktionen ein mit ihrem Verhalten.</Paragraph>
<div class="w-full min-h-96">
	<ResultGraph datasets={plotData} labels={plotLabels} />
</div>
  