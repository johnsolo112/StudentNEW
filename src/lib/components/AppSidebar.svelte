<script lang="ts">
	import { browser } from '$app/environment';
	import { page } from '$app/stores';
	import { loadStudentInfo } from '$lib/cache';
	import { studentInfo } from '$lib/stores';
	import {
		Sidebar,
		SidebarBrand,
		SidebarGroup,
		SidebarItem,
		SidebarWrapper
	} from 'flowbite-svelte';
	import {
		AddressBookOutline,
		AnnotationOutline,
		ArrowRightToBracketOutline,
		BellOutline,
		FileLinesOutline,
		FolderOpenOutline,
		MailBoxOutline,
		UserCircleOutline
	} from 'flowbite-svelte-icons';

	function logOut() {
		localStorage.clear();
		location.assign('/login');
	}

	if (!$studentInfo && browser) loadStudentInfo();
</script>

<Sidebar activeUrl={$page.url.pathname} class="h-screen">
	<SidebarWrapper class="h-screen flex flex-col justify-between">
		<SidebarGroup>
			<SidebarBrand
				site={{
					name: 'BetterVue',
					href: '/grades',
					img: '/favicon.svg'
				}}
			/>

			<SidebarItem label="Grades" href="/grades">
				<svelte:fragment slot="icon">
					<AddressBookOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>

			<SidebarItem label="Attendance" href="/attendance">
				<svelte:fragment slot="icon">
					<BellOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>

			<SidebarItem label="Report Cards" href="/reportcards">
				<svelte:fragment slot="icon">
					<FileLinesOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>

			<SidebarItem label="Documents" href="/documents">
				<svelte:fragment slot="icon">
					<FolderOpenOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>

			<SidebarItem label="Messages" href="/messages">
				<svelte:fragment slot="icon">
					<MailBoxOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>
		</SidebarGroup>

		<SidebarGroup>
			<SidebarItem label="Feedback" href="/feedback">
				<svelte:fragment slot="icon">
					<AnnotationOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>

			<SidebarItem label={$studentInfo?.FormattedName ?? ''} href="/studentinfo">
				<svelte:fragment slot="icon">
					<UserCircleOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>

			<SidebarItem on:click={logOut} label="Log Out" href="/login">
				<svelte:fragment slot="icon">
					<ArrowRightToBracketOutline class="focus:outline-none" />
				</svelte:fragment>
			</SidebarItem>
		</SidebarGroup>
	</SidebarWrapper>
</Sidebar>
