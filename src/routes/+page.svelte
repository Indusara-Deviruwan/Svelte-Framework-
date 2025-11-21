<script>
	import { onDestroy } from "svelte";

	/* Auto-changing banner images */
	let banners = [
		"/banner1.jpg",
		"/banner2.jpg",
		"/banner3.jpg",
		"/banner4.jpg"
	];

	let current = 0;

	// Auto-change banner every 4 seconds
	const interval = setInterval(() => {
		current = (current + 1) % banners.length;
	}, 4000);

	// Stop interval on page unload
	onDestroy(() => clearInterval(interval));
</script>

<!-- ===========================
        AUTO CHANGING BANNER
=========================== -->
<section class="relative w-full h-[360px] md:h-[480px] overflow-hidden rounded-xl mb-12">

	{#each banners as banner, i}
		<img
			src={banner}
			alt="Travel Banner"
			class="absolute inset-0 w-full h-full object-cover object-top rounded-xl transition-opacity duration-1000"
			style="opacity: {current === i ? 1 : 0};"
		/>
	{/each}

	<!-- Overlay Text -->
	<div
		class="absolute inset-0 flex flex-col items-center justify-center text-center px-4"
		style="color: var(--bg); background: rgba(0,0,0,0.35);"
	>
		<h1 class="text-4xl md:text-5xl font-bold drop-shadow-lg">
			Explore Sri Lanka With Us
		</h1>

		<p class="mt-3 max-w-xl text-lg drop-shadow-md opacity-90">
			Comfortable, safe, and unforgettable travel experiences.
		</p>

	</div>
</section>

<!-- ===========================
		WELCOME SECTION
===========================	-->
<section
	class="flex flex-col items-center justify-center text-center gap-6 py-20 px-4 transition"
	style="color: var(--text);"
>
	<h1 class="text-4xl font-bold">Welcome to 2nd Chance Travels</h1>

	<p class="text-lg max-w-xl opacity-80">
		Your trusted travel partner — explore Sri Lanka with the best service and comfort.
	</p>

	<!-- Example hero button -->
	<a
		href="/services"
		class="mt-4 px-6 py-3 rounded-xl font-semibold transition hover:scale-105"
		style="background-color: var(--text); color: var(--bg);"
	>
		Explore Our Services
	</a>
</section>

<section class="px-6 py-16 transition" style="color: var(--text);">
	<h2 class="text-2xl font-semibold mb-6">Why Choose Us?</h2>

	<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
		<div class="p-6 rounded-xl shadow-md transition"
			style="background-color: var(--bg); border: 1px solid var(--text);"
		>
			<h3 class="font-bold text-xl mb-2">Experienced Guides</h3>
			<p class="opacity-80">Professional and friendly tour guides with local expertise.</p>
		</div>

		<div class="p-6 rounded-xl shadow-md transition"
			style="background-color: var(--bg); border: 1px solid var(--text);"
		>
			<h3 class="font-bold text-xl mb-2">Comfortable Vehicles</h3>
			<p class="opacity-80">Clean, well-maintained vehicles for a smooth journey.</p>
		</div>

		<div class="p-6 rounded-xl shadow-md transition"
			style="background-color: var(--bg); border: 1px solid var(--text);"
		>
			<h3 class="font-bold text-xl mb-2">Affordable Packages</h3>
			<p class="opacity-80">Travel plans that fit your budget without compromising quality.</p>
		</div>
	</div>
</section>
