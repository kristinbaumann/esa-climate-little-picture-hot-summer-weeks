<script lang="ts">
	import data from '../data/temp_country_weekly_median_column.json';

	const days = data.Date;
	const weekTempCountry = data.DE;
	console.log('weekTempCountry', weekTempCountry);
</script>

<div>
	<p>Chart</p>
	<svg width="2000" height="2000">
		<g transform={`translate(10,10)`}>
			{#each weekTempCountry as weekTemp, i}
				<circle
					cx={15 * (i % 53)}
					cy={Math.floor(i / 53) * 15}
					r="5"
					fill="black"
					stroke="black"
					aria-label={`${i}-${days[i]}`}
				/>
			{/each}
		</g>
	</svg>
</div>
