<script lang="ts">
	import data from '../data/temp_country_weekly_max_daily_in_week_all_countries_new.json';
	//import data from '../data/temp_subcountry_ES30_weekly_max_daily_in_week.json';

	import { scaleSequential } from 'd3-scale';
	import { interpolateReds } from 'd3-scale-chromatic';

	let countryNames = [
		'AL',
		// 'AT',
		'BA',
		'BE',
		'BG',
		// 'CH',
		'CY',
		// 'CZ',
		'DE',
		// 'DK',
		// 'EE',
		'EL', // Greece
		'ES',
		// 'FI',
		'FR',
		'HR',
		'HU',
		// 'IE',
		// 'IS',
		'IT',
		'LT',
		'LU',
		'LV',
		'ME',
		'MK',
		'NL',
		// 'NO',
		'PL',
		'PT',
		'RO',
		'RS',
		// 'SE',
		'SI',
		'SK',
		'TR'
		// 'UK'
	]; // no data for LI and MT

	countryNames = ['SK'];
	const colorGrey = '#dfdfdf';
	const distanceBetweenCircles = 4;
	const radius = 5;
	const minTemp = 20.5;

	const test = data.map((d: any) => Number(d['SK']));
	const maxTemp = Math.max.apply(Math, test);
	console.log(maxTemp);

	//const color = scaleSequential(interpolateReds).domain([minTemp, maxTemp]);
	const color = scaleSequential(interpolateReds).domain([minTemp - 0.5, maxTemp - 0.5]);

	function getFill(temp: number) {
		if (temp < minTemp) return colorGrey;
		return color(temp);
	}

	function getStroke(temp: number) {
		if (temp < minTemp) return colorGrey;
		return color(temp);
	}
	function getRadius(temp: number) {
		if (temp < minTemp) return 1;
		return radius;
	}
</script>

{#each countryNames as countryName}
	<svg width="920" height="950" style={'background-color: #FFFCED;'}>
		<!-- <g transform={`translate(15,15)`}>
			<text>{countryName}</text>
		</g> -->
		<g transform={`translate(15,25)`}>
			{#each data as entry}
				{#if entry.weeknumber !== 53 && entry.year > 1979 && entry.year < 2023}
					<circle
						cx={(radius * 2 + distanceBetweenCircles) * entry.weeknumber}
						cy={(entry.year - 1979) * (radius * 2 + distanceBetweenCircles * 2)}
						r={getRadius(Number(entry[countryName]))}
						aria-label={`${entry.year} ${entry.weeknumber} ${entry[countryName]}`}
						fill={getFill(Number(entry[countryName]))}
						stroke={getStroke(Number(entry[countryName]))}
					/>
				{/if}
			{/each}
		</g>
	</svg>
{/each}
