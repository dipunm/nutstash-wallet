<script lang="ts">
	import { THEMES } from '../stores/static/themes';

	import { theme } from '../stores/theme';
	import BackupButton from './elements/BackupButton.svelte';
	import NostrRelayModal from './elements/NostrRelayModal.svelte';
	import NostrSettings from './elements/NostrSettings.svelte';
	import ResetHistoryButton from './elements/ResetHistoryButton.svelte';

	let isShowDangerzone = false

	const setTheme = (t: string) => {
		theme.set(t);
	};
</script>

<div class="flex flex-col justify-start gap-3 w-full">
	<div class="grid grid-cols-5 w-full items-center gap-2 overflow-y-scroll">
		<p class="text-xl font-bold col-span-5">Settings</p>
		<div class="-span-1">
			<label for="theme-dropdown">Theme:</label>
		</div>
		<div class="dropdown col-span-4" id="theme-dropdown">
			<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
			<!-- svelte-ignore a11y-label-has-associated-control -->
			<label tabindex="0" class="btn">{$theme}</label>
			<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
			<ul
				tabindex="0"
				class="dropdown-content menu p-2 shadow bg-base-100 rounded-box w-52 max-h-56 overflow-scroll"
			>
				<!-- svelte-ignore a11y-missing-attribute -->
				{#each THEMES as theme}
					<!-- svelte-ignore a11y-missing-attribute -->
					<!-- svelte-ignore a11y-click-events-have-key-events -->
					<li on:click={() => setTheme(theme)}><a>{theme}</a></li>
				{/each}
			</ul>
		</div>
		<div class="col-span-1">
			<label for="">Backup Tokens</label>
		</div>
		<div class="col-span-4">
			<BackupButton />
		</div>
		<div class="col-span-1">
			<label for="">Restore from Backup</label>
		</div>
		<div class="col-span-4">
			<a href="/restore" class="btn btn-primary">restore</a>
		</div>
		<div class="col-span-1">
			<label for="">History</label>
		</div>
		<div class="col-span-4">
			<a href="/history" class="btn btn-outline">History</a>
		</div>
		<div  class="divider col-span-5">Nostr</div>

		<NostrSettings></NostrSettings>
		<div  class="divider col-span-5 flex">
			<div>
				<button on:click={()=>isShowDangerzone=!isShowDangerzone}>
					<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 transition-transform {isShowDangerzone?'rotate-90':''}">
						<path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
					  </svg>
					  
				</button>
			</div>
			<p>
				Dangerzone
			</p>
		</div>
		{#if isShowDangerzone}
		<div class="col-span-1">
			<label for="delete-history-button">Delete History</label>
		</div>
		<div class="col-span-4">
			<ResetHistoryButton />
		</div>
		{/if}
	</div>
</div>
<NostrRelayModal></NostrRelayModal>