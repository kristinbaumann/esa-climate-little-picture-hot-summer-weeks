<script lang="ts">
	import data from '../data/temp_country_weekly_max_daily_in_week_all_countries.json';

	const countryNames = [
		'AL',
		'AT',
		'BA',
		'BE',
		'BG',
		'CH',
		'CY',
		'CZ',
		'DE',
		'DK',
		'EE',
		'EL',
		'ES',
		'FI',
		'FR',
		'HR',
		'HU',
		'IE',
		'IS',
		'IT',
		'LT',
		'LU',
		'LV',
		'ME',
		'MK',
		'NL',
		'NO',
		'PL',
		'PT',
		'RO',
		'RS',
		'SE',
		'SI',
		'SK',
		'TR',
		'UK'
	]; // no data for LI and MT
	//const countryName = 'BE';

	// import { scaleLinear } from 'd3-scale';
	// import { interpolateSpectral } from 'd3-scale-chromatic';

	// const tempAsNumber = data.map((d: any) => Number(d.max_daily_in_week));

	// const myScale = scaleLinear()
	// 	.domain([Math.min.apply(Math, tempAsNumber), Math.max.apply(Math, tempAsNumber)])
	// 	.range([1, 0]);

	function getColor(temp: number) {
		// return interpolateSpectral(myScale(temp));

		if (temp > 25) {
			return 'darkred';
		}
		if (temp > 20) {
			return 'indianred';
		}
		return '#eeeeee';
	}
</script>

{#each countryNames as countryName}
	<svg width="1500" height="750">
		<g transform={`translate(15,15)`}>
			<text>{countryName}</text>
		</g>
		<g transform={`translate(5,25)`}>
			{#each data as entry, i}
				{#if entry.weeknumber !== 53 && entry.year < 2023}
					<circle
						cx={15 * entry.weeknumber}
						cy={(entry.year - 1979) * 15}
						r="5"
						aria-label={`${entry.year} ${entry.weeknumber} ${entry[countryName]}`}
						fill={getColor(Number(entry[countryName]))}
					/>
				{/if}
			{/each}
		</g>
	</svg>
{/each}
