<script lang="ts">
	import { onMount } from 'svelte';
	import Chart from 'chart.js/auto';
	import 'chartjs-adapter-date-fns';
	
	export let chart_data: Array < Object >;

	let canvas: any;

	const data = {
		labels: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
		datasets: [
			{
				label: '1',
				data: [11, 15, 18, 35, 99, 54, 33, 32, 23, 76],
				/**data: chart_data,
				parsing: {
					xAxisKey: 'DATE',
					yAxisKey: 'SWAP_VOLUME'
				},**/
				backgroundColor: ['#2A9D8F'] //, '#2A9D8F', '#E9C46A', '#F4A261', '#E76F51']
			}
		]
	};
	onMount(() => {
		const ctx = canvas.getContext('2d');
		var chart = new Chart(ctx, {
			type: 'bar',
			data: data,
			options: {
				indexAxis: 'y',
				maintainAspectRatio: false,
				responsive: true,
				scales: {
					y: {
						reverse: false,
						border: {
							display: true,
							color: 'black',
							width: 1
						},
						grid: {
							display: false
						}
					},
					x: {
						title: {
							display: true,
							text: 'Amount',
							font: {
								size: 15,
								family: "'Quicksand', 'sans-serif",
							},
							color: 'black',
							padding: 10
						},
						border: {
							display: true,
							color: 'black',
							width: 1
						}
					}
				},
				elements : {
					point: {
						pointStyle: false
					},
					line: {
						fill: false
					}
				},
				
				plugins: {
					legend: {
						display: false,
						position: 'right',
						align: 'start',
						labels: {
							usePointStyle: true,
							pointStyle: 'circle'
						}
					},
					tooltip: {
						padding: 10,
						boxPadding: 3,
						titleAlign: 'center',
						titleMarginBottom: 6
					}
				},
				interaction: {
					intersect: false,
					mode: 'nearest',
					axis: 'y'
				}
			}
		});
	});
</script>

<canvas bind:this={canvas} class="pr-2"/>
