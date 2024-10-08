<script lang="ts">
	import { browser } from '$app/environment';
	import { goto } from '$app/navigation';
	import { studentAccount } from '$lib/stores';
	import { StudentAccount } from '$lib/synergy';
	import { Button, Card } from 'flowbite-svelte';
	import {
		ChartOutline,
		ClockOutline,
		EyeSlashOutline,
		GithubSolid,
		GridPlusOutline
	} from 'flowbite-svelte-icons';

	if (browser && localStorage.getItem('token')) {
		if (!$studentAccount) {
			const { username, password, domain } = JSON.parse(localStorage.getItem('token') ?? '{}');
			$studentAccount = new StudentAccount(domain, username, password);
		}

		goto('/grades');
	}
</script>

<svelte:head>
	<title>BetterVue - The best way to check your grades on StudentVue</title>
</svelte:head>

<div class="p-4 flex flex-col gap-4 items-center justify-center min-h-screen">
	<Card class="w-full sm:w-auto">
		<h1 class="text-2xl font-bold tracking-tight text-gray-900 dark:text-white">BetterVue</h1>
		<p class="mt-2 font-normal text-gray-700 dark:text-gray-400">
			An better way to view your grades on StudentVue that shows all of your Synergy information in
			one place.
		</p>
		<div class="mt-4 flex space-x-4">
			<Button href="/login" color="light" class="w-full">Log in</Button>
			
		</div>
	</Card>

	<div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
		<Card>
			<h2 class="text-xl dark:text-white mb-2 flex items-center gap-2">
				<ChartOutline class="inline focus:outline-none" />
				Grade Calculator
			</h2>
			<p>
				BetterVue's powerful Hypothetical Mode allows you to calculate what your grade would be if
				you got a score on an assignment, as well as how each assignment affects your grade.
			</p>
		</Card>
		<Card>
			<h2 class="text-xl dark:text-white mb-2 flex items-center gap-2">
				<GridPlusOutline class="inline focus:outline-none" />
				Shows Hidden Assignments
			</h2>
			<p>
				BetterVue is able to reveal hidden assignments and will factor them into your grade
				calculations. You never have to worry about your grade calculations being inaccurate!
			</p>
		</Card>
		<Card>
			<h2 class="text-xl dark:text-white mb-2 flex items-center gap-2">
				<EyeSlashOutline class="inline focus:outline-none" />
				Private Login
			</h2>
			<p>
				BetterVue does not have access to your login information. When you use BetterVue, your device
				connects directly to StudentVue. We never see your password or your grades!
				<a href="/privacy" class="text-primary-600 underline">Learn more</a>
			</p>
		</Card>
		<Card>
			<h2 class="text-xl dark:text-white mb-2 flex items-center gap-2">
				<ClockOutline class="inline focus:outline-none" />
				Attendance and more
			</h2>
			<p>
				BetterVue breaks down your attendance by day and shows what periods you missed. It also
				shows your report cards, documents, and messages.
			</p>
		</Card>
	</div>

	<Button
		href="https://github.com/johnsolo112BetterVue"
		target="_blank"
		color="light"
		class="gap-2"
	>
		<GithubSolid class="inline focus:outline-none" />
		Open Source
	</Button>
</div>
