<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();

	let scrolled = $state(false);
	let menuOpen = $state(false);

	const navLinks = [
		{ label: 'Who We Are', href: '#who-we-are' },
		{ label: 'Beliefs', href: '#beliefs' },
		{ label: 'Voices', href: '#voices' },
		{ label: 'Resources', href: '#resources' },
		{ label: 'Connect', href: '#connect' }
	];

	function handleScroll() {
		scrolled = window.scrollY > 80;
	}

	function closeMenu() {
		menuOpen = false;
	}
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<svelte:window onscroll={handleScroll} />

<div class="grain">
	<!-- Navigation -->
	<nav
		class="fixed top-0 left-0 right-0 z-50 transition-all duration-500"
		class:nav-scrolled={scrolled}
		class:nav-top={!scrolled}
	>
		<div class="mx-auto flex max-w-7xl items-center justify-between px-6 py-4">
			<a
				href="/"
				class="flex items-center gap-2 transition-all duration-300"
			>
				<img src={favicon} alt="Reimagining Schools Collective" class="h-8 w-8 md:h-9 md:w-9" />
				<span
					class="font-display text-lg font-bold tracking-tight md:text-xl"
					class:text-paper={!scrolled}
					class:text-ink={scrolled}
				>RSC</span>
			</a>

			<!-- Desktop nav -->
			<div class="hidden items-center gap-8 md:flex">
				{#each navLinks as link (link.href)}
					<a
						href={link.href}
						class="font-hand text-lg transition-all duration-300 hover:scale-105 hover:text-ochre"
						class:text-paper={!scrolled}
						class:text-ink={scrolled}
					>
						{link.label}
					</a>
				{/each}
			</div>

			<!-- Mobile menu button -->
			<button
				class="flex flex-col gap-1.5 md:hidden"
				onclick={() => (menuOpen = !menuOpen)}
				aria-label="Toggle menu"
			>
				<span
					class="block h-0.5 w-6 transition-all duration-300"
					class:bg-paper={!scrolled}
					class:bg-ink={scrolled}
					class:translate-y-2={menuOpen}
					class:rotate-45={menuOpen}
				></span>
				<span
					class="block h-0.5 w-6 transition-all duration-300"
					class:bg-paper={!scrolled}
					class:bg-ink={scrolled}
					class:opacity-0={menuOpen}
				></span>
				<span
					class="block h-0.5 w-6 transition-all duration-300"
					class:bg-paper={!scrolled}
					class:bg-ink={scrolled}
					class:-translate-y-2={menuOpen}
					class:-rotate-45={menuOpen}
				></span>
			</button>
		</div>

		<!-- Mobile menu -->
		{#if menuOpen}
			<div class="bg-paper/95 backdrop-blur-sm md:hidden">
				<div class="flex flex-col gap-4 px-6 pb-6">
					{#each navLinks as link (link.href)}
						<a
							href={link.href}
							class="font-hand text-ink text-xl transition-colors hover:text-terracotta"
							onclick={closeMenu}
						>
							{link.label}
						</a>
					{/each}
				</div>
			</div>
		{/if}
	</nav>

	{@render children()}
</div>

<style>
	.nav-top {
		background: transparent;
	}

	.nav-scrolled {
		background: rgba(253, 246, 236, 0.92);
		backdrop-filter: blur(12px);
		box-shadow: 0 2px 20px rgba(43, 45, 66, 0.08);
	}
</style>
