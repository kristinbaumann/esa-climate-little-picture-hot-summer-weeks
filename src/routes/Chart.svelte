<script lang="ts">
	import data from '../data/temp_country_weekly_mean_week_aggregation_start_monday.json';

	import { scaleLinear } from 'd3-scale';
	import { interpolateSpectral } from 'd3-scale-chromatic';

	const tempAsNumber = data.map((d: any) => Number(d.DE));

	const myScale = scaleLinear()
		.domain([Math.min.apply(Math, tempAsNumber), Math.max.apply(Math, tempAsNumber)])
		.range([1, 0]);
</script>

<svg width="2000" height="2000">
	<g transform={`translate(10,10)`}>
		{#each data as entry, i}
			{#if entry.weeknumber !== 53 && entry.year < 2023}
				<circle
					cx={15 * entry.weeknumber}
					cy={(entry.year - 1979) * 15}
					r="5"
					aria-label={`${entry.year} ${entry.weeknumber} ${entry.DE}`}
					fill={interpolateSpectral(myScale(Number(entry.DE)))}
				/>
			{/if}
		{/each}
	</g>
</svg>
