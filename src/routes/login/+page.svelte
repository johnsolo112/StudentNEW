<script lang="ts">
	import { browser } from '$app/environment';
	import { goto } from '$app/navigation';
	import LoadingBanner from '$lib/components/LoadingBanner.svelte';
	import { studentAccount } from '$lib/stores';
	import { StudentAccount } from '$lib/synergy';
	import {
		Accordion,
		AccordionItem,
		Alert,
		Button,
		Card,
		Helper,
		Input,
		Label
	} from 'flowbite-svelte';
	import {
		ExclamationCircleSolid,
		EyeSlashOutline,
		InfoCircleOutline
	} from 'flowbite-svelte-icons';
	import { fly } from 'svelte/transition';

	if (browser && localStorage.getItem('token')) {
		if (!$studentAccount) {
			const { username, password, domain } = JSON.parse(localStorage.getItem('token') ?? '{}');
			$studentAccount = new StudentAccount(domain, username, password);
		}

		goto('/grades');
	}

	let username: string;
	let password: string;
	let domain: string = 'ca-nhu.edupoint.com';

	let loginErrorShown = false;
	let loginError: string;

	let loggingIn = false;

	async function login() {
		if (loggingIn) return;
		loggingIn = true;

		const loginAccount = new StudentAccount(domain, username, password);

		try {
			await loginAccount.checkLogin();
		} catch (e) {
			loggingIn = false;

			loginErrorShown = true;
			loginError = e instanceof Error ? e.message : 'An unknown error occurred';
			return;
		}

		$studentAccount = loginAccount;

		localStorage.setItem('token', JSON.stringify({ username, password, domain }));

		loggingIn = false;

		goto('/grades');
	}
</script>

<svelte:head>
	<title>Log In - BetterVue</title>
</svelte:head>

<LoadingBanner show={loggingIn} loadingMsg="Logging you in..." />

{#if loginErrorShown}
	<div in:fly={{ y: -50, duration: 200 }} class="fixed w-full p-4 top-0 left-0 flex justify-center">
		<Alert color="red">
			<ExclamationCircleSolid slot="icon" />
			<span class="font-bold">Couldn't log in</span>
			<p>{loginError}</p>
		</Alert>
	</div>
{/if}

<div class="flex items-center justify-center min-h-screen">
	<Card>
		<form on:submit|preventDefault={login}>
			<h1 class="text-xl mb-4 dark:text-white">Sign in to BetterVue</h1>
			<Label class="space-y-2 mb-4">
				<span>Username</span>
				<Input
					type="text"
					id="username"
					bind:value={username}
					placeholder="josmith"
					required
				/>
			</Label>
			<Label class="space-y-2 mb-4">
				<span>Password</span>
	
				<Input type="password" id="password" bind:value={password} class="mb-2"  placeholder="Google Password" required />
				<Helper class="text-xs flex items-center">
					<EyeSlashOutline size="sm" class="mr-2 focus:outline-none" />
					Your device connects directly to StudentVue. We can't see your password or your grades.
				</Helper>
				
			</Label>
			
			
			<Button type="submit" class="w-full">Log in</Button>
		</form>
	</Card>
</div>
