<script lang="ts">
	import ButtonBlue from '$lib/components/ButtonBlue.svelte';
    import Heading2 from '$lib/components/Heading2.svelte';
	import Heading3 from '$lib/components/Heading3.svelte';
	import Paragraph from '$lib/components/Paragraph.svelte';
	import UnorderedList from '$lib/components/UnorderedList.svelte';
    import { t } from '$lib/translations/i18n';
    import { goto } from '$app/navigation';
	import type { PageData } from './$types';
	import { PUBLIC_ADMIN_MAIL } from '$env/static/public';
    export let data: PageData;
</script>

<Paragraph>Dieses Tool bietet psychoanalytische Auswertungen aufgrund eines Fragebogens in folgenden Kategorien:</Paragraph>
<UnorderedList>
    {#each data.categories as category}
    <li>{category.label}</li>
    {/each}
</UnorderedList>
<Paragraph customClass="pt-3 pb-5">Der Fragebogen kann für beliebige Kombinationen von Kategorien ausgefüllt werden. Sie können den Fragebogen mit oder ohne Login ausfüllen. Falls Sie mehrere Fragebogen ausfüllen wollen, lohnt es sich, ein Konto zu erstellen und anschliessend einzuloggen. Einzelne Resultate werden dann nebeneinander dargestellt.</Paragraph>
<ButtonBlue on:callback={() => { goto("/questionnaire"); }}>Zum Fragebogen</ButtonBlue>
<Heading2 customClass="pt-8">{$t('home.sources')}</Heading2>
<UnorderedList>
    <li>Karl Kälin, Peter Müri (2020): "Sich und andere führen", <a href="http://www.touchdown.ch/pages/egogram.html">www.touchdown.ch/pages/egogram.html</a>, 8.1.2024</li>
    <li>Silvio Sgier (2006): "Die inneren Stressmacher", <a href="https://www.radix.ch/media/ci2hsf11/impulstagung-sngs-2006_sgier_die-inneren-stressmacher.pdf">www.radix.ch/media/ci2hsf11/impulstagung-sngs-2006_sgier_die-inneren-stressmacher.pdf</a>, 8.1.2024</li>
    <li>Margot Ruprecht, Benno Greter: "Fragebogen zum Mini-Skript und Antreiberverhalten", Version erhalten am 11.10.2024</li>
    <li>Benno Greter, Thomas Meier: "Fragebogen zur Transaktionsanalyse: Rollen im Drama-Dreieck", 23.1.2024</li>
    <li>Tara Hanke, Enneagramm-Test, <a href="https://coachinglovers.com/enneagramm/enneagramm-test/">https://coachinglovers.com/enneagramm/enneagramm-test/</a>, 29.4.2024</li>
    <li>Felix C. Brodbeck, Neil Anderson, Michael A. West (2000): "Das Teamklima-Inventar Handanweisung", <a href="https://www.psy.uni-muenchen.de/wirtschaftspsychologie_en/forschung/working_paper/wop_working_paper_2000_2.pdf">https://www.psy.uni-muenchen.de/wirtschaftspsychologie_en/forschung/working_paper/wop_working_paper_2000_2.pdf</a>, 21.5.2024</li>
</UnorderedList>
<Heading2 customClass="pt-8">Umgang mit Daten</Heading2>
<Paragraph>Falls Sie sich einloggen, sind von Ihnen ausgefüllte Fragebogen mit Ihrem Konto verlinkt. Sie können für jedes Resultat auswählen, ob Sie dieses einem Team zugänglich machen wollen oder nicht. Teams haben höchstens Zugriff auf Ihre Auswertungen, nie auf Antworten auf einzelne Fragen.</Paragraph>
<Paragraph>Ohne Login werden Fragebögen anonymisiert gespeichert. Der von Ihnen gewählte Name des Fragebogens ist, falls Sie das Resultat mit einem Team teilen, für das Team ersichtlich.</Paragraph>
<Paragraph>Bei Fragen wenden Sie sich an <a href="mailto:{PUBLIC_ADMIN_MAIL}">{PUBLIC_ADMIN_MAIL}</a>.</Paragraph>
<Heading2 customClass="pt-8">Netzwerk Kanton Bern</Heading2>
<Heading3>Sanität Notruf</Heading3>
<Paragraph><a href="tel:144">T 144 (24h)</a></Paragraph>
<Heading3>Polizei Notruf</Heading3>
<Paragraph><a href="tel:117">T 117 (24h)</a></Paragraph>
<Heading3>Vergiftungsnotfälle</Heading3>
<Paragraph><a href="tel:145">T 145 (24h)</a><br /><a href="https://www.toxinfo.ch/">www.toxinfo.ch</a></Paragraph>
<Heading3>Telefon 1811</Heading3>
<Paragraph>Gibt Auskunft, welcher Arzt in der Region Notfalldienst hat, welche Apotheke in der Nähe
Notfalldienst hat und welches Spital sich in der Nähe befindet (24h).</Paragraph>
<Heading3>Die Dargebotene Hand</Heading3>
<Paragraph><a href="tel:143">Beratung für Erwachsene: Tel. 143 (24h)</a><br /><a href="https://www.143.ch/">www.143.ch</a></Paragraph>
<Heading3>Berner Gesundheit</Heading3>
<Paragraph>Gesundheitsförderung, Prävention, Sexualpädagogik sowie Suchtberatung und -therapie. Mit vier Regionalzentren und zusätzlichen Standorten im ganzen Kanton Bern vertreten.</Paragraph>
<Paragraph><a href="tel:0800070070">T 0800 070 070</a><br /><a href="https://www.bernergesundheit.ch/">www.bernergesundheit.ch</a></Paragraph>
<Heading3>Kriseninterventionszentrum KIZ Bern</Heading3>
<Paragraph>Die Angebote des Kriseninterventionszentrums (KIZ) am Standort der UPD beim Inselspital richten sich an Erwachsene, die sich in einer psychosozialen Krise befinden, beispielsweise nach einer Trennung, in einer Trauerphase oder aufgrund von Ängsten.</Paragraph>
<Paragraph>Murtenstrasse 21<br />3008 Bern<br /><a href="tel:0316328811">T 031 632 88 11</a></Paragraph>
<Heading3>UPD Universitätsklinik für Psychiatrie und Psychotherapie</Heading3>
<Paragraph>Kinder und Jugendliche<br />Regionen Bern Mittelland, Oberaargau/Emmental und Oberland<br />24h / 7 Tage geöffnet</Paragraph>
<Paragraph>Notfallzentrum NZKJP T <a href="tel:0319328844">031 932 88 44</a></Paragraph>
<Paragraph>Erwachsene <a href="tel:0316328811">T 031 632 88 11</a></Paragraph>
<Heading3><a href="https://www.psy.ch">psy.ch</a></Heading3>
<Paragraph>Wegweiser für psychische Gesundheit im Kanton Bern, der den niederschwelligen Zugang zu Hilfsangeboten erleichtert. Mit psy.ch steht eine Webseite zur Verfügung, welche die vielen Angebote im Kanton Bern übersichtlich darstellt und die wichtigsten Fragen zu psychischer Gesundheit beantwortet. Unter «Angebote» finden sich weitere 358 Angebote des Kantons Bern.</Paragraph>
<Paragraph>Interessengemeinschaft Sozialpsychiatrie Bern<br />Holzikofenweg 22<br />3007 Bern<br /><a href="tel:0313707976">T 031 370 79 76</a></Paragraph>
<Heading3>Beratungsstelle Opferhilfe Bern</Heading3>
<Paragraph>Die Opferhilfe bietet Information und Beratung, Vermittlung von Fachpersonen sowie Sofortmassnahmen und langfristige Unterstützung.</Paragraph>
<Paragraph>Seftigenstrasse 41<br />3007 Bern<br />Telefon: <a href="tel:0313703070">031 370 30 70</a><br /><a href="mailto:beratungsstelle@opferhilfe-bern.ch">beratungsstelle@opferhilfe-bern.ch</a></Paragraph>
<Heading3>Berner Interventionsstelle gegen Häusliche Gewalt</Heading3>
<Paragraph>Ratsuchende erreichen die Berner Interventionsstelle während der Bürozeiten. Sie bietet verschiedene Broschüren zum Thema an. Die Notfallkarten, die in 14 Sprachen erhältlich sind, enthalten die wichtigsten Adressen der Hilfe- und Unterstützungsangebote des Kantons Bern.</Paragraph>
<Paragraph>Kramgasse 20<br />3011 Bern<br />Telefon: <a href="tel:0316335033">031 633 50 33</a><br /><a href="mailto:info.big@pom.be.ch">info.big@pom.be.ch</a></Paragraph>
<Heading3>Fachstelle Gewalt Bern</Heading3>
<Paragraph>Die Fachstelle Gewalt Bern engagiert sich für eine gewaltfreie Gesellschaft im Kanton Bern. Kernaufgabe ist die Beratung und Therapie von gewalttätigen Menschen. Gearbeitet wird im Einzelsetting.</Paragraph>
<Paragraph>Seilerstrasse 25<br />3011 Bern<br />Telefon: <a href="tel:0313817506">031 381 75 06</a><br /><a href="mailto:info@fachstellegewalt.ch">info@fachstellegewalt.ch</a></Paragraph>
<Heading3>Selbsthilfe BE</Heading3>
<Paragraph>Beratungszentrum Bern<br />Beratung und Information für Hilfesuchende, Interessierte und Fachpersonen rund um das Thema Selbsthilfe.</Paragraph>
<Paragraph>Bollwerk 41<br />3011 Bern<br />Telefon: <a href="tel:0848339900">0848 33 99 00</a><br /><a href="mailto:info@selbsthilfe-be.ch">info@selbsthilfe-be.ch</a></Paragraph>
<Heading2 customClass="pt-8">Weiterführende Links zum Thema psychosoziale Fragebögen, alle am 21.5.2024 abgerufen:</Heading2>
<UnorderedList>
    <li>Sammlung von diversen psychologischen Tests: Leibniz-Institut für Psychologie (ZPID). (2019). Open Test Archive. Startseite. Verfügbar unter: <a href="https://www.testarchiv.eu/">www.testarchiv.eu</a></li>
    <li>Online ausfüllbare, mehrheitlich frei erhältliche Tests: <a href="https://www.psychomeda.de/online-tests/">www.psychomeda.de/online-tests/</a></li>
    <li>Tool mit Sammlung von Psychologischen Diagnostik Testverfahren: <a href="https://psydix.org/de/">https://psydix.org/de/</a></li>
    <li>Teamwork Big Five Questionnaire for Hybrid and Remote teams: <a href="https://www.researchgate.net/publication/375671814_Team_effectiveness_survey_Development_and_validation_of_the_Teamwork_Big_Five_Questionnaire_for_HybridRemote_teams_2023">www.researchgate.net/publication/375671814_Team_effectiveness_survey_Development_and_validation_of_the_Teamwork_Big_Five_Questionnaire_for_HybridRemote_teams_2023</a></li>
    <li>Tests des Hogrefe-Verlags: <a href="https://www.testzentrale.ch/">www.testzentrale.ch</a></li>
    <li>PCM-Test: <a href="https://test2.thepersonalitylab.org/">https://test2.thepersonalitylab.org/</a></li>
    <li>Test zu Persönlichkeitsstärken der UZH: <a href="https://www.persoenlichkeitsstaerken.ch/">www.persoenlichkeitsstaerken.ch</a></li>
    <li>DISG-Persönlichkeitstest (und weitere Tests unter demselben Link): <a href="https://www.123test.com/de/DISG-Pers%C3%B6nlichkeitstest/">https://www.123test.com/de/DISG-Pers%C3%B6nlichkeitstest/</a></li>
    <li>Google Re:Work Studie zu effizienten Teams: <a href="https://www.linkedin.com/pulse/5-keys-successful-google-team-project-aristotle-julian-pawley-lkecc">www.linkedin.com/pulse/5-keys-successful-google-team-project-aristotle-julian-pawley-lkecc</a> und <a href="https://www.thinkwithgoogle.com/intl/en-emea/consumer-insights/consumer-trends/five-dynamics-effective-team/">www.thinkwithgoogle.com/intl/en-emea/consumer-insights/consumer-trends/five-dynamics-effective-team/</a></li>
</UnorderedList>