<script lang="ts">
	import SidebarDropdown from './SidebarDropdown.svelte';
	import type { SidebarType } from '../types';
	export let links: SidebarType[];

	export let childClass: string = 'flex items-center p-2 pl-11 w-full text-base font-normal text-gray-900 rounded-lg transition duration-75 group hover:bg-gray-100 dark:text-white dark:hover:bg-gray-700';

	export let dropDownulClass: string = 'py-2 space-y-2';

	let ulClass = 'space-y-2';
	export let border: boolean = false;
	if (border) {
		ulClass = 'pt-4 mt-4 space-y-2 border-t border-gray-200 dark:border-gray-700';
	}
</script>

<ul class={ulClass}>
	{#each links as link (link.id)}
		{#if link.children}
			<SidebarDropdown {link} ulClass={dropDownulClass} {childClass} />
		{:else}
			<li>
				<a href={link.href} rel={link.rel} class="flex items-center p-2 text-base font-normal text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700">
					{#if link.icon}
						<svelte:component this={link.icon} size={link.iconSize} color={link.iconColor} class="mr-2 {link.iconClass}" />
					{/if}
					<span class="ml-3">{link.name}</span>
					{#if link.subtext}
						{@html link.subtext}
					{/if}
				</a>
			</li>
		{/if}
	{/each}
</ul>
