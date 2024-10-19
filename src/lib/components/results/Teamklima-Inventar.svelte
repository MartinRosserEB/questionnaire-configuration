<script lang="ts">
	import type { ResultGraphDataSets } from "$lib/custom-types";
	import ResultGraph from "$lib/components/ResultGraph.svelte";
  import Select from 'svelte-select';

  export let plotData: ResultGraphDataSets;
  export let plotLabels: string[];

  class tkiSubCategory {
    label: string;
    max: number;
    mean: number | null = null;
    numArray: number[] = [];

    constructor (label: string, max: number) {
      this.label = label;
      this.max = max;
    }

    add (num: number) {
      this.numArray.push(num);
      this.resetMean();
    }

    computeMean () : number {
      if (this.mean === null) {
        this.mean = this.numArray.reduce((acc, val) => acc + val, 0) / this.numArray.length;
      }
      return this.mean;
    }

    getMean () : string {
      return this.computeMean().toLocaleString('de-CH', { minimumFractionDigits: 1, maximumFractionDigits: 1 });
    }

    resetMean () : void {
      this.mean = null;
    }

    getStdDev () : string {
      let stdDev = this.numArray.length > 1 ? Math.sqrt(
        this.numArray.reduce((acc, val) => acc + ((val - this.computeMean()) ** 2), 0) /
        (this.numArray.length - 1)).toLocaleString('de-CH', { minimumFractionDigits: 1, maximumFractionDigits: 1 }) : '-';
      return stdDev;
    }

    getStaNine () : string {
      let i = 0, continueLoop = true, lookupTable = stanineLookupTables[selectedStanineCategory.value][this.label], outputString = '-';
      if (typeof lookupTable !== 'undefined') {
        while (i < lookupTable.length && continueLoop === true) {
          if (this.getMean() < lookupTable[i]) {
            continueLoop = false;
          } else {
            i++;
          }
        }
        outputString = (i+1).toString();
      }
      return outputString;
    }
  }

  class tkiCategory {
    label: string;
    subCategories: tkiSubCategory[];
    mean: number | null = null;

    constructor (label: string, subCatArr: tkiSubCategory[]) {
      this.label = label;
      this.subCategories = subCatArr;
    }

    computeMean () : number {
      if (this.mean === null) {
        let valArr: number[] = [];
        this.subCategories.forEach(subCat => {
          valArr.push(subCat.computeMean());
        });
        this.mean = valArr.reduce((acc, val) => acc + val, 0);
      }
      return this.mean;
    }

    getMean () : string {
      return this.computeMean().toLocaleString('de-CH', { minimumFractionDigits: 1, maximumFractionDigits: 1 });
    }

    getStdDev () : string {
      let valArr: number[] = [];
      this.subCategories.forEach(subCat => {
        if (valArr.length === 0) {
          valArr = structuredClone(subCat.numArray);
        } else {
          for (let i = 0; i < subCat.numArray.length; i++) {
            valArr[i] += subCat.numArray[i];
          }
        }
      });
      return valArr.length > 1 ? Math.sqrt(valArr.reduce((acc, val) => acc + (val - this.computeMean()) ** 2, 0) / (valArr.length - 1)).toLocaleString('de-CH', { minimumFractionDigits: 1, maximumFractionDigits: 1 }) : '-';
    }

    getMax () : string {
      let sum = 0;
      this.subCategories.forEach(subCat => sum += subCat.max);
      return (sum ).toLocaleString('de-CH', { minimumFractionDigits: 1, maximumFractionDigits: 1 });
    }

    getStaNine () : string {
      let i = 0, continueLoop = true, lookupTable = stanineLookupTables[selectedStanineCategory.value][this.label], outputString = '-';
      if (typeof lookupTable !== 'undefined') {
        while (i < lookupTable.length && continueLoop === true) {
          if (this.getMean() < lookupTable[i]) {
            continueLoop = false;
          } else {
            i++;
          }
        }
        outputString = (i+1).toString();
      }
      return outputString;
    }
  }

  const teamklimaStructure = [
    new tkiCategory('Vision',
      [
        new tkiSubCategory('Klarheit',10),
        new tkiSubCategory('Wertschätzung',20),
        new tkiSubCategory('Einigkeit',15),
        new tkiSubCategory('Erreichbarkeit',10)
      ]),
    new tkiCategory('Aufgabenorientierung',
      [
        new tkiSubCategory('Hohe Standards',10),
        new tkiSubCategory('Reflexion',15),
        new tkiSubCategory('Synergie',10)
      ]),
    new tkiCategory('Partizipative Sicherheit',
      [
        new tkiSubCategory('Informationsverteilung',15),
        new tkiSubCategory('Sicherheit',10),
        new tkiSubCategory('Einfluss',15),
        new tkiSubCategory('Kontaktpflege',20)
      ]),
    new tkiCategory('Unterstützung für Innovation',
      [
        new tkiSubCategory('Bereitschaft',20),
        new tkiSubCategory('Umsetzung',20)
      ]),
    new tkiCategory('Soziale Erwünschtheit',
      [
        new tkiSubCategory('Soziale Aspekte',15),
        new tkiSubCategory('Aufgabenaspekte',15)
      ])
  ];

  let stanineCategories = [
    {
      "value": 0,
      "label": "Industrie und Verwaltung"
    },
    {
      "value": 1,
      "label": "Pflege und Betreuung"
    },
    {
      "value": 2,
      "label": "Produkt- und Software-Entwicklung"
    },
    {
      "value": 3,
      "label": "Planspielgruppen"
    }
  ];
  const stanineLookupTables = [
    {
      "Vision": [36.9, 38.4, 39.8, 43.0, 44.5, 45.6, 47.2, 48.3],
      "Klarheit": [5.3, 6.8, 7.0, 7.7, 7.9, 8.4, 8.8, 9.3],
      "Wertschätzung": [13.6, 14.4, 15.5, 16.2, 16.7, 17.2, 17.8, 18.1],
      "Einigkeit": [9.4, 10.0, 10.8, 11.2, 11.9, 12.5, 12.9, 13.2],
      "Erreichbarkeit": [6.5, 6.7, 7.2, 7.7, 8.0, 8.2, 8.6, 9.3],
      "Aufgabenorientierung": [20.9, 22.1, 23.6, 25.4, 27.3, 28.5, 29.3, 30.0],
      "Hohe Standards": [5.6, 5.9, 6.9, 7.4, 8.0, 8.3, 8.7, 8.9],
      "Reflexion": [9.2, 9.9, 10.1, 10.9, 11.5, 11.8, 12.2, 12.8],
      "Synergie": [5.5, 6.0, 7.0, 7.3, 7.8, 8.3, 8.5, 8.8],
      "Partizipative Sicherheit": [34.5, 36.4, 40.1, 42.7, 45.1, 49.5, 51.2, 52.6],
      "Informationsverteilung": [8.7, 8.8, 9.5, 11.1, 11.7, 12.4, 12.6, 13.7],
      "Sicherheit": [5.4, 6.3, 6.5, 7.0, 7.9, 8.1, 8.6, 8.8],
      "Einfluss": [8.2, 8.4, 9.7, 10.3, 11.4, 11.7, 12.1, 12.4],
      "Kontaktpflege": [11.5, 12.6, 13.3, 14.1, 15.3, 17.1, 17.9, 18.5],
      "Unterstützung für Innovation": [21.5, 22.7, 25.2, 26.8, 28.4, 30.6, 32.0, 33.4],
      "Bereitschaft": [11.0, 11.5, 12.9, 13.6, 14.4, 15.2, 15.9, 16.4],
      "Umsetzung": [10.5, 11.0, 12.3, 13.2, 13.9, 15.3, 16.3, 17.1]
    },
    {
      "Vision": [35.1, 38.6, 39.9, 42.1, 43.3, 44.4, 45.1, 47.6],
      "Klarheit": [6.0, 6.7, 7.2, 7.6, 8.0, 8.2, 8.6, 9.0],
      "Wertschätzung": [13.8, 14.3, 15.1, 15.8, 16.4, 16.8, 17.6, 17.8],
      "Einigkeit": [9.3, 10.5, 10.6, 11.3, 11.8, 12.0, 12.2, 12.5],
      "Erreichbarkeit": [5.9, 6.2, 6.4, 7.0, 7.6, 7.8, 8.0, 8.7],
      "Aufgabenorientierung": [17.3, 21.0, 23.9, 25.8, 27.4, 28.5, 29.4, 30.6],
      "Hohe Standards": [5.1, 5.8, 6.8, 7.3, 7.7, 8.3, 8.6, 9.0],
      "Reflexion": [7.1, 9.0, 10.1, 10.9, 11.2, 12.1, 12.5, 13.0],
      "Synergie": [5.1, 6.1, 7.0, 7.3, 8.1, 8.5, 8.8, 8.9],
      "Partizipative Sicherheit": [37.0, 39.8, 41.6, 44.6, 48.4, 51.1, 52.5, 55.3],
      "Informationsverteilung": [10.1, 11.0, 11.7, 12.2, 12.7, 13.5, 13.8, 13.9],
      "Sicherheit": [4.6, 5.9, 6.4, 7.0, 7.8, 8.3, 8.8, 9.3],
      "Einfluss": [9.6, 10.0, 10.2, 10.9, 12-0, 12.4, 13.0, 13.6],
      "Kontaktpflege": [11.1, 12.3, 13.1, 14.2, 16.1, 16.9, 18.1, 18.8],
      "Unterstützung für Innovation": [21.1, 22.6, 24.4, 26.2, 27-8, 30.5, 31.9, 33.6],
      "Bereitschaft": [11.0, 11.2, 12.1, 13.2, 14.0, 15.2, 15.9, 16.8],
      "Umsetzung": [10.0, 11.3, 12.0, 12.8, 14.1, 15.1, 16.4, 16.8]
    },
    {
      "Vision": [32.9, 38.8, 40.5, 41.7, 42.4, 44.3, 46.7, 49.8],
      "Klarheit": [6.9, 7.3, 7.7, 7.9, 8.2, 8.6,  9.0, 9.3],
      "Wertschätzung": [10.3, 12.9, 13.8, 14.6, 15.3, 16.1, 16.8, 17.9],
      "Einigkeit": [8.9, 10.4, 11.0, 11.3, 11.7, 12.2, 12.7, 14.1],
      "Erreichbarkeit": [5.9, 6.7, 7.2, 7.6,  8.0, 8.4, 8.7, 8.9],
      "Aufgabenorientierung": [17.1, 22.4, 23.5, 25.0, 26.8, 27.9, 29.3, 30.6],
      "Hohe Standards": [4.3, 6.0, 6.5, 7.0, 7.3, 7.8, 8.6, 9.0],
      "Reflexion": [7.6, 9.0, 10.2, 10.8, 11.5, 12.0, 12.7, 13.2],
      "Synergie": [5.2, 6.5, 7.0, 7.4, 7.9, 8.3, 8.7, 9.0],
      "Partizipative Sicherheit": [38.0, 41.6, 43.3, 45.7, 47.9, 49.1, 51.4, 54.8],
      "Informationsverteilung": [9.7, 10.2, 11.0, 11.7, 12.3, 12.7, 13.3, 13.8],
      "Sicherheit": [6.0, 6.3, 7.0, 7.2, 7.8, 8.0,  8.8, 9.2],
      "Einfluss": [9.3, 10.1, 10.8, 11.6, 12.0, 12.3, 13.0, 13.9],
      "Kontaktpflege": [12.8, 13.3, 14.3, 14.9, 15.9, 16.6, 17.5, 18.5],
      "Unterstützung für Innovation": [20.6, 24.2, 26.3, 28.4, 30.0, 31.3, 32.4, 34.8],
      "Bereitschaft": [11.1, 12.3, 13.5, 14.0, 15.2, 15.8, 16.4, 17.8],
      "Umsetzung": [9.5, 11.9, 12.9, 14.2, 15.1, 15.6, 16.0, 17.0]
    },
    {
      "Vision": [36.4, 37.7, 40.9, 42.6, 44.3, 45.3, 46.5, 48.7],
      "Klarheit": [7.1, 7.6, 8.0, 8.6, 9.0, 9.2, 9.3, 9.7],
      "Wertschätzung": [10.8, 12.3, 13.2, 13.7, 14.5, 15.1, 16.0, 17.3],
      "Einigkeit": [9.1, 10.7, 11.3, 12.3, 13.0, 13.4, 13.7, 14.5],
      "Aufgabenorientierung": [19.5, 22.5, 26.2, 27.3, 28.3, 29.6, 31.0, 31.9],
      "Hohe Standards": [4.8, 6.2, 7.0, 7.8, 8.0, 8.4, 9.0, 9.3],
      "Reflexion": [8.3, 9.7, 11.0, 11.7, 12.3, 12.8, 13.3, 13.7],
      "Synergie": [6.4, 6.7, 7.6, 7.8, 8.3, 8.8, 9.3, 9.4],
      "Partizipative Sicherheit": [37.1, 41.8, 45.5, 48.7, 50.3, 53.3, 54.8, 55.6],
      "Informationsverteilung": [8.8, 10.6, 11.6, 12.7, 13.3, 13.8, 14.3, 14.6],
      "Sicherheit": [6.0, 6.5, 7.6, 8.0, 8.5, 9.1, 9.5, 10.0],
      "Einfluss": [9.7, 10-8, 11.3, 11.8, 12.7, 13.3, 13.7, 14.0],
      "Kontaktpflege": [11.7, 12-7, 14.2, 15.6, 16.3, 17.4, 18.1, 18.9],
      "Unterstützung für Innovation": [20.3, 25.3, 28.4, 29.7, 31.8, 32.7, 34.0, 35.3],
      "Bereitschaft": [10.0, 12.8, 14.0, 14.7, 15.3, 16.4, 17.0, 17.3],
      "Umsetzung": [10.3, 12.3, 14.3, 15.0, 15.7, 16.8, 17.5, 17.8]
    }
  ]
  let selectedStanineCategory = stanineCategories[0];

  $: {
    plotData.forEach(pd => {
      plotLabels.forEach((label, index) => {
        teamklimaStructure.forEach(tks => {
          const tksScRes = tks.subCategories.find(tksSc => tksSc.label === label);
          if (typeof tksScRes !== 'undefined') {
            tksScRes.add(pd.data[index]);
          }
        });
      });
    });
  }
</script>

<p>Stanine berechnen für Kategorie:</p>
<Select bind:items={stanineCategories} bind:value={selectedStanineCategory} />
{#key selectedStanineCategory}
<table class="table-auto w-full mb-3">
  <thead class="border-b border-neutral-200">
    <tr>
      <th class="px-2 text-left">Kategorie</th>
      <th class="px-2 text-left">Unterkategorie</th>
      <th class="px-2 text-right">&mu; / max.</th>
      <th class="px-2 text-right">&sigma;</th>
      <th class="px-2 text-right">Stanine</th>
    </tr>
  </thead>
  <tbody>
    {#each teamklimaStructure as teamKlima}
    <tr class="border-b border-neutral-200">
      <td colspan=2 class="px-2 font-bold">{teamKlima.label}</td>
      <td class="text-right px-2 font-bold">{teamKlima.getMean()} / {teamKlima.getMax()}</td>
      <td class="text-right px-2 font-bold">{teamKlima.getStdDev()}</td>
      <td class="text-right px-2 font-bold">{teamKlima.getStaNine()}</td>
    </tr>
    {#each teamKlima.subCategories as tkiSubCat}
    <tr class="border-b border-neutral-200">
      <td />
      <td class="px-2">{tkiSubCat.label}</td>
      <td class="text-right px-2">{tkiSubCat.getMean()} / {tkiSubCat.max}</td>
      <td class="text-right px-2">{tkiSubCat.getStdDev()}</td>
      <td class="text-right px-2">{tkiSubCat.getStaNine()}</td>
    </tr>
    {/each}
    {/each}
  </tbody>
</table>
{/key}
<div class="w-full min-h-96">
	<ResultGraph datasets={plotData} labels={plotLabels} />
</div>
