<script lang="ts">
	import "../app.css";
	import { onMount } from "svelte";
	import logo from "$lib/assets/2nd chance logo.png";

	let theme: "light" | "dark" = "light";

	onMount(() => {
		const saved = localStorage.getItem("theme");
		const sysDark = window.matchMedia("(prefers-color-scheme: dark)").matches;

		theme = saved ? (saved as "light" | "dark") : sysDark ? "dark" : "light";
		applyTheme();
	});

	function applyTheme() {
		document.documentElement.classList.toggle("dark", theme === "dark");
		localStorage.setItem("theme", theme);
	}

	function toggleTheme() {
		theme = theme === "light" ? "dark" : "light";
		applyTheme();
	}
</script>

<svelte:head>
	<link rel="icon" href={logo} />
</svelte:head>

<header class="flex justify-end items-center p-4 transition"
	style="background-color: var(--bg); color: var(--text);"
>

	<button
		on:click={toggleTheme}
		class="p-2 rounded-full transition hover:scale-105"
		style="background-color: var(--bg); color: var(--text); border: 1px solid var(--text);"
	>
		{#if theme === "light"}
			<!-- Moon -->
			<svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2">
				<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
			</svg>
		{:else}
			<!-- Sun -->
			<svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2">
				<circle cx="12" cy="12" r="4" />
				<path
					d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41
					M2 12h2M20 12h2M4.93 19.07l1.41-1.41M17.66 6.34l1.41-1.41"
				/>
			</svg>
		{/if}
	</button>
</header>

<main class="min-h-screen p-4 transition"
	style="background-color: var(--bg); color: var(--text);"
>
	<slot />
</main>
