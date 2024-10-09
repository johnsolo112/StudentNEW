<script lang="ts">
	import { browser } from '$app/environment';
	import { Card } from 'flowbite-svelte';

	let email = '[email protected]';
	if (browser) email = 'jsolo112@proton.me;
</script>

<svelte:head>
	<title>Privacy - BetterVue</title>
</svelte:head>

<div class="flex items-center justify-center min-h-screen">
	<Card size="lg" class="gap-4">
		<h1 class="text-2xl text-white">About the privacy of BetterVue</h1>
		<p>
			 BetterVue is designed to keep students' information private the entire
			time you use the service. It's similar to using the StudentVue app; even though you're not
			viewing the offical website, you're still accessing your grades securely, just in a more
			convenient manner.
		</p>

		<p>
			When a student logs in to BetterVue, their username and password are sent directly to the
			offical website, using the built-in
			<a
				href="https://ca-nhu.edupoint.com/Service/PXPCommunication.asmx"
				class="text-primary-600 underline"
			>
				Synergy API
			</a>.
		</p>

		<span>
			If you have questions or concerns about BetterVue, please contact me at
			<a href="mailto:{email}" class="text-primary-600 underline">{email}</a>.
		</span>
	</Card>
</div>
