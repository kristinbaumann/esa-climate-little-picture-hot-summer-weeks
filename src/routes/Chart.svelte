<script lang="ts">
	import data from '../data/temp_country_weekly_median_column.json';
	import { scaleLinear } from 'd3-scale';
	import { schemeGreens, interpolateSpectral } from 'd3-scale-chromatic';

	const scale = schemeGreens[6];

	const days = data.Date;
	const weekTempCountry = data.DE;

	const tempAsNumber = weekTempCountry.map((d: String) => Number(d));
	console.log('temp', tempAsNumber, interpolateSpectral(1));

	const myScale = scaleLinear()
		.domain([Math.min.apply(Math, tempAsNumber), Math.max.apply(Math, tempAsNumber)])
		.range([1, 0]);
</script>

<svg width="2000" height="2000">
	<g transform={`translate(10,10)`}>
		{#each tempAsNumber as weekTemp, i}
			<circle
				cx={15 * (i % 52)}
				cy={(new Date(days[i]).getFullYear() - 1979) * 15}
				r="5"
				fill={interpolateSpectral(myScale(weekTemp))}
				aria-label={`${i}-${days[i]}-${weekTemp}`}
			/>
			<!-- aria-label={`${1980-}`} -->
		{/each}
	</g>
</svg>
