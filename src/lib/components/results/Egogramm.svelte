<script lang="ts">
	import Heading3 from "$lib/components/Heading3.svelte";
  import Paragraph from "$lib/components/Paragraph.svelte";
	import ResultGraph from "$lib/components/ResultGraph.svelte";
  import type { ResultGraphDataSets } from "$lib/custom-types";

  export let plotData: ResultGraphDataSets;
  export let plotLabels: string[];

</script>

<Paragraph>Ein Egogramm ist eine grafische Analyse, das Aufschluss über die Verteilung der jeweiligen Ich-Zustände einer Person gibt. Es geht vor allem darum herauszufinden, wie viel Zeit man in den jeweiligen Zuständen verbringt.</Paragraph>
<Paragraph>Die Ich-Zustände stellen ein zentrales Konzept in der Transaktionsanalyse dar. Mit ihnen kannst du bestimmen, in welchem Zustand du und andere sich befinden. Das wird im Egogramm ausgewertet. Wir fokussieren uns in dieser Übung mehr auf deine Ich-Zustände als die der anderen.</Paragraph>
<Paragraph>Ein Ich-Zustand ist ein spezifisches Muster in der  Kombination aus Denken, Fühlen und Verhalten. Es gibt folgende Ich-Zustände.</Paragraph>
<Heading3>Das fürsorgliche Eltern-Ich</Heading3>
<Paragraph>Das fürsorgliche Eltern-Ich im Positiven: Wenn du beispielsweise deinen traurigen Partner nach einem Verlust in den Arm nimmst oder wenn jemand in Not ist und du hilfst ihm.</Paragraph>
<Paragraph>Das fürsorgliche Eltern-Ich im Negativen: Wenn du deinen Partner 15 Mal am Tag anrufst, um dich nach seinen Befinden zu erkundigen und ihn damit erdrückst oder sonst auf andere Art überfürsorglich bist.</Paragraph>
<Heading3>Das kritische Eltern-Ich</Heading3>
<Paragraph>Das kritische Eltern-Ich im Positiven: Du übst konstruktive Kritik oder wenn du deinen eigenen Kindern Regeln und damit Orientierung bietest. Auch als Führungskraft kann es passieren, dass Du für die Einhaltung von Regeln sorgen musst. Zum Beispiel, wenn jemand seine Schutzkleidung nicht trägt, obwohl dies dringend geboten wär.</Paragraph>
<Paragraph>Das kritische Eltern-Ich im Negativen: Du beschimpfst und kritisierst deine Mitarbeiter unangemessen oder suchst ständig Fehler bei deinem Partner.</Paragraph>
<Heading3>Das Erwachsenen-Ich</Heading3>
<Paragraph>Das Erwachsenen-Ich wird nicht weiter unterteilt. Es wird angenommen als eine Reaktion aus dem Hier und Jetzt, die auch angemessen erscheint. Beispielsweise bei einer sachlichen Diskussion unter Freunden oder bei der Planung der bevorstehenden Arbeit. Manche Transaktionsanalytiker unterteilen es auch in positive und negative Aspekte. Ein negativer Aspekt könnte in einer allzu rationalen Reaktion auf eine emotionale Reaktion liegen.</Paragraph>
<Heading3>Das angepasste und das rebellische Kind-Ich</Heading3>
<Paragraph>Das angepasste Kind im Positiven: Du wurdest wegen eines defekten Rücklichts von der Polizei angehalten und zeigst einsichtiges Verhalten.</Paragraph>
<Paragraph>Das angepasste Kind im Negativen: Wenn du überangepasst bist, zu allem “Ja” sagst und keine eigene Meinung mehr hast.</Paragraph>
<Paragraph>Das rebellische Kind im Positiven: Wenn du deine Grenzen erkundest, zum Beispiel, indem du dich traust “Nein” zu sagen.</Paragraph>
<Paragraph>Das rebellische Kind im Negativen: Wenn du zum Beispiel beleidigt oder trotzig mit deinem Partner bist und dich nicht mit ihm auseinandersetzt. Oder, wenn du im Beruf deine Führungskraft an die Wand laufen lässt, weil du jetzt nur noch auf Anweisungen reagierst.</Paragraph>
<Paragraph>Das freie Kind im Positiven: Wenn jemand ausgelassen mit einem Hund spielt oder die Pflanzenwelt neugierig erkundet. Wenn jemand nach einem Verlust traurig ist, oder Angst hat, wenn ihm ein Tiger begegnet oder wütend ist, wenn jemand in seine Wohnung eingebrochen ist.</Paragraph>
<Paragraph>Das freie Kind im Negativen: Wenn du es nicht ertragen kannst, dass du nicht deinen Willen bekommst. Oder du unangemessen lustig bist, während alle ander Sorgen haben. Das mündet in einer gewissen Egozentrik.</Paragraph>
<div class="w-full min-h-96">
  <ResultGraph datasets={plotData} labels={plotLabels} />
</div>
