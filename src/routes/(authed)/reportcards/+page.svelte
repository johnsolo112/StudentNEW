<script lang="ts">
	import { browser } from '$app/environment';
	import { loadReportCardList } from '$lib/cache';
	import DateBadge from '$lib/components/DateBadge.svelte';
	import LoadingBanner from '$lib/components/LoadingBanner.svelte';
	import { reportCardList, reportCardListLoaded } from '$lib/stores';
	import { Badge, Card } from 'flowbite-svelte';

	if (!$reportCardList && browser) loadReportCardList();
</script>

<svelte:head>
	<title>Report Cards - BetterVue</title>
</svelte:head>

<LoadingBanner show={!$reportCardListLoaded} loadingMsg="Loading report cards..." />

{#if $reportCardList}
	<ol class="p-4 space-y-4">
		{#each $reportCardList as reportCard}
			<li>
				{#if reportCard._DocumentGU}
					<Card
						href="/documents/{reportCard._DocumentGU}"
						class="dark:text-white max-w-none flex-row items-center gap-2"
					>
						<h2 class="text-xl">{reportCard._ReportingPeriodName}</h2>
						<DateBadge date={new Date(reportCard._EndDate)} />
					</Card>
				{:else}
					<Card class="dark:text-white max-w-none flex-row items-center gap-2">
						<h2 class="text-xl">{reportCard._ReportingPeriodName}</h2>
						<DateBadge date={new Date(reportCard._EndDate)} />
						<Badge color="red">PDF not available</Badge>
					</Card>
				{/if}
			</li>
		{/each}
	</ol>
{/if}
