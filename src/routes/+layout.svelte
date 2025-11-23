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

<!-- ===========================
          HEADER
=========================== -->
<header
	class="flex items-center justify-between p-4 shadow-md transition sticky top-0 z-50"
	style="background-color: var(--bg); color: var(--text);"
>
	<!-- Logo + Name -->
	<div class="flex items-center gap-3">
		<img src={logo} alt="Logo" class="h-10 w-auto rounded" />
		<h1 class="text-xl font-bold">2nd Chance Travels</h1>
	</div>

	<!-- Navigation -->
	<nav class="hidden md:flex gap-6 font-semibold">
		<a href="/" class="hover:opacity-70 transition">Home</a>
		<a href="/services" class="hover:opacity-70 transition">Services</a>
		<a href="/about" class="hover:opacity-70 transition">About</a>
		<a href="/contact" class="hover:opacity-70 transition">Contact</a>
	</nav>

	<!-- Theme Toggle Button -->
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

<!-- ===========================
            MAIN CONTENT
=========================== -->
<main
	class="min-h-screen p-4 transition pt-6"
	style="background-color: var(--bg); color: var(--text);"
>
	<slot />
</main>

<!-- ===========================
            FOOTER
=========================== -->
<footer
	class="mt-12 py-8 text-center transition border-t"
	style="background-color: var(--bg); color: var(--text); border-color: var(--text);"
>
	<p class="font-semibold text-lg">2nd Chance Travels</p>
	<p class="opacity-75 mt-1">Your trusted travel partner in Sri Lanka.</p>

	<div class="flex justify-center gap-6 mt-4">
		<a href="/" class="hover:opacity-70">Home</a>
		<a href="/services" class="hover:opacity-70">Services</a>
		<a href="/about" class="hover:opacity-70">About</a>
		<a href="/contact" class="hover:opacity-70">Contact</a>
	</div>

	<p class="opacity-60 text-sm mt-6">© {new Date().getFullYear()} 2nd Chance Travels. All rights reserved.</p>
</footer>
