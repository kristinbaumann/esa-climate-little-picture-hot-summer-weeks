<script lang="ts">
	import data from '../data/temp_country_weekly_max_daily_in_week_all_countries.json';

	import { scaleSequential } from 'd3-scale';
	import { interpolateReds } from 'd3-scale-chromatic';

	const countryName = 'SK';

	// dots
	const distDots = 4;
	const radiusDots = 5;
	const mutedColorDots = '#dfdfdf';

	// chart variables
	const startYear = 1979;
	const endYear = 2023;

	const chartWidth = (radiusDots * 2 + distDots) * 53; // 742
	const chartHeight = (endYear - 1 - startYear) * (radiusDots * 2 + distDots * 2) + distDots * 2; // 782

	// vis variables
	const minTemp = 20.5;
	const temperatures = data.map((d: any) => Number(d[countryName]));
	const maxTemp = Math.max.apply(Math, temperatures);

	const color = scaleSequential(interpolateReds).domain([minTemp - 0.5, maxTemp - 0.5]);

	function getFill(temp: number) {
		if (temp < minTemp) return mutedColorDots;
		return color(temp);
	}

	function getStroke(temp: number) {
		if (temp < minTemp) return mutedColorDots;
		return color(temp);
	}
	function getRadius(temp: number) {
		if (temp < minTemp) return 1;
		return radiusDots;
	}
</script>

<svg width={chartWidth} height={chartHeight} style={'background-color: #FFFCED;'}>
	<g transform={`translate(0,-${distDots})`}>
		{#each data as d}
			{#if d.weeknumber !== 53 && d.year > startYear && d.year < endYear}
				<circle
					cx={(radiusDots * 2 + distDots) * d.weeknumber}
					cy={(d.year - startYear) * (radiusDots * 2 + distDots * 2)}
					r={getRadius(Number(d[countryName]))}
					fill={getFill(Number(d[countryName]))}
					stroke={getStroke(Number(d[countryName]))}
					aria-label={`${d.year} ${d.weeknumber}`}
				/>
			{/if}
		{/each}
	</g>
</svg>
