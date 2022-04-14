<script context="module">
	import { t, locales, locale, loadTranslations } from '$lib/translations';

	export const load = async ({ url }) => {
		const { pathname } = url;

		const defaultLocale = 'en'; // get from cookie, user session, ...

		const initLocale = locale.get() || defaultLocale; // set default if no locale already set

		await loadTranslations(initLocale, pathname); // keep this just before the `return`

		return {};
	};
</script>

<script lang="ts">
	import Header from '$lib/header/Header.svelte';

	const link = 'https://kit.svelte.dev';

	import '../app.css';
</script>

<Header />

<main>
	<slot />

	<select bind:value={$locale}>
		{#each $locales as value}
			<option {value}>{$t(`lang.${value}`)}</option>
		{/each}
	</select>
</main>

<footer>
	<p>{@html $t('common.text', { link })}</p>
</footer>

<style>
	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 1024px;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	}
</style>
