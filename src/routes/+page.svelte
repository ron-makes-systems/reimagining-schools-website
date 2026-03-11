<script lang="ts">
	import { onMount } from 'svelte';

	let mounted = $state(false);

	onMount(() => {
		mounted = true;
	});

	// Scroll reveal action
	function reveal(node: HTMLElement) {
		node.classList.add('reveal');
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						node.classList.add('revealed');
						observer.unobserve(node);
					}
				});
			},
			{ threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
		);
		observer.observe(node);
		return {
			destroy() {
				observer.disconnect();
			}
		};
	}

	function revealLeft(node: HTMLElement) {
		node.classList.add('reveal-left');
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						node.classList.add('revealed');
						observer.unobserve(node);
					}
				});
			},
			{ threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
		);
		observer.observe(node);
		return {
			destroy() {
				observer.disconnect();
			}
		};
	}

	function revealRight(node: HTMLElement) {
		node.classList.add('reveal-right');
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						node.classList.add('revealed');
						observer.unobserve(node);
					}
				});
			},
			{ threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
		);
		observer.observe(node);
		return {
			destroy() {
				observer.disconnect();
			}
		};
	}

	const accentColors: Record<string, string> = {
		terracotta: '#c75b39',
		teal: '#1a6b5a',
		magenta: '#b44b8c',
		ochre: '#e8a838',
		coral: '#e87461',
		sage: '#87a878'
	};

	const voices = [
		{
			text: "We're not waiting for permission to imagine a different kind of school. We're building it, right now, with our hands and our hearts.",
			author: 'Amara, 16',
			location: 'Nairobi, Kenya',
			accent: 'terracotta'
		},
		{
			text: "Learning doesn't stop at the classroom door. My grandmother's garden taught me more about ecosystems than any textbook ever could.",
			author: 'Mateo, Teacher',
			location: 'Bogota, Colombia',
			accent: 'teal'
		},
		{
			text: 'When we center imagination, we don\'t lose rigor \u2014 we find purpose. We find the reason to keep going.',
			author: 'Dr. Priya Sharma',
			location: 'Mumbai, India',
			accent: 'magenta'
		},
		{
			text: 'I see the world differently, and that is not a deficit. My neurodivergent mind is a gift to reimagining what learning can be.',
			author: 'Sam, 14',
			location: 'Auckland, Aotearoa',
			accent: 'ochre'
		},
		{
			text: 'Art is how we remember what matters. Every mural, every poem, every song is a curriculum of the soul.',
			author: 'Fatima, Artist-Educator',
			location: 'Dakar, Senegal',
			accent: 'coral'
		},
		{
			text: 'The ancestors knew: learning is ceremony. It is relational. It is alive. We are remembering what was always there.',
			author: 'Uncle Kev',
			location: 'Bundjalung Country, Australia',
			accent: 'sage'
		}
	];

	const beliefs = [
		{ text: 'All of life is a place of learning', color: '#c75b39' },
		{ text: 'Youth voices drive meaningful change', color: '#1a6b5a' },
		{ text: 'Transform from the root', color: '#b44b8c' },
		{ text: 'Reorient toward life, liberation & equity', color: '#e8a838' },
		{ text: 'Imagination reshapes reality', color: '#e87461' },
		{ text: 'Hold liminality and emergence with reverence', color: '#9b8ec4' }
	];

	const resources = [
		{
			title: 'Poetry & Words',
			desc: 'Verses from young poets and elders across the collective',
			color: 'magenta',
			icon: 'M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253'
		},
		{
			title: 'Visual Art',
			desc: 'Murals, collages, and illustrations reimagining learning spaces',
			color: 'terracotta',
			icon: 'M9.53 16.122a3 3 0 0 0-5.78 1.128 2.25 2.25 0 0 1-2.4 2.245 4.5 4.5 0 0 0 8.4-2.245c0-.399-.078-.78-.22-1.128Zm0 0a15.998 15.998 0 0 0 3.388-1.62m-5.043-.025a15.994 15.994 0 0 1 1.622-3.395m3.42 3.42a15.995 15.995 0 0 0 4.764-4.648l3.876-5.814a1.151 1.151 0 0 0-1.597-1.597L14.146 6.32a15.996 15.996 0 0 0-4.649 4.763m3.42 3.42a6.776 6.776 0 0 0-3.42-3.42'
		},
		{
			title: 'Activity Ideas',
			desc: 'Creative prompts and activities for learning communities everywhere',
			color: 'teal',
			icon: 'M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z'
		},
		{
			title: 'Dialogue Prompts',
			desc: 'Conversation starters for reimagining education together',
			color: 'ochre',
			icon: 'M20.25 8.511c.884.284 1.5 1.128 1.5 2.097v4.286c0 1.136-.847 2.1-1.98 2.193-.34.027-.68.052-1.02.072v3.091l-3-3c-1.354 0-2.694-.055-4.02-.163a2.115 2.115 0 0 1-.825-.242m9.345-8.334a2.126 2.126 0 0 0-.476-.095 48.64 48.64 0 0 0-8.048 0c-1.131.094-1.976 1.057-1.976 2.192v4.286c0 .837.46 1.58 1.155 1.951m9.345-8.334V6.637c0-1.621-1.152-3.026-2.76-3.235A48.455 48.455 0 0 0 11.25 3c-2.115 0-4.198.137-6.24.402-1.608.209-2.76 1.614-2.76 3.235v6.226c0 1.621 1.152 3.026 2.76 3.235.577.075 1.157.14 1.74.194V21l4.155-4.155'
		},
		{
			title: 'Workbooks',
			desc: 'Co-created guides for community-led learning design',
			color: 'sage',
			icon: 'M19.5 14.25v-2.625a3.375 3.375 0 0 0-3.375-3.375h-1.5A1.125 1.125 0 0 1 13.5 7.125v-1.5a3.375 3.375 0 0 0-3.375-3.375H8.25m0 12.75h7.5m-7.5 3H12M10.5 2.25H5.625c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125V11.25a9 9 0 0 0-9-9Z'
		},
		{
			title: 'Community Stories',
			desc: 'Narratives from learning communities transforming from within',
			color: 'coral',
			icon: 'M21 8.25c0-2.485-2.099-4.5-4.688-4.5-1.935 0-3.597 1.126-4.312 2.733-.715-1.607-2.377-2.733-4.313-2.733C5.1 3.75 3 5.765 3 8.25c0 7.22 9 12 9 12s9-4.78 9-12Z'
		}
	];

	const rotations = [-2.5, 1.8, -1.2, 3, -0.8, 2.2];
</script>

<svelte:head>
	<title>Reimagining Schools Collective</title>
	<meta
		name="description"
		content="An intergenerational, global collective of educators, artists, youth, and imaginative minds reimagining what learning can be."
	/>
</svelte:head>

<!-- ===== HERO ===== -->
<section class="hero-section">
	<!-- Floating organic shapes -->
	<div class="hero-blob blob-1" class:blob-animate={mounted}></div>
	<div class="hero-blob blob-2" class:blob-animate={mounted}></div>
	<div class="hero-blob blob-3" class:blob-animate={mounted}></div>
	<div class="hero-blob blob-4" class:blob-animate={mounted}></div>
	<div class="hero-blob blob-5" class:blob-animate={mounted}></div>

	<!-- Decorative scattered elements -->
	<div class="hero-scatter scatter-1" class:scatter-animate={mounted}>~</div>
	<div class="hero-scatter scatter-2" class:scatter-animate={mounted}>*</div>
	<div class="hero-scatter scatter-3" class:scatter-animate={mounted}>&</div>

	<div class="hero-content" class:hero-visible={mounted}>
		<p class="hero-kicker font-hand">a living, breathing, co-created space</p>
		<h1 class="hero-title font-display">
			<span class="hero-title-line">Reimagining</span>
			<span class="hero-title-line hero-title-accent">Schools</span>
			<span class="hero-title-line">Collective</span>
		</h1>
		<p class="hero-subtitle font-body">
			An intergenerational, global gathering of educators, artists,
			<br class="hidden md:block" />
			youth & imaginative minds — from all continents.
		</p>
		<p class="hero-whisper font-hand">We are alive. We are growing. We are many.</p>
	</div>

	<!-- Scroll indicator -->
	<div class="scroll-indicator" class:scroll-visible={mounted}>
		<div class="scroll-line"></div>
	</div>
</section>

<!-- ===== WHO WE ARE ===== -->
<section id="who-we-are" class="relative overflow-hidden px-6 py-24 md:py-36">
	<!-- Organic section divider -->
	<div class="section-wave">
		<svg viewBox="0 0 1440 120" fill="none" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
			<path
				d="M0,60 C240,120 480,0 720,60 C960,120 1200,0 1440,60 L1440,120 L0,120 Z"
				fill="currentColor"
			/>
		</svg>
	</div>

	<div class="mx-auto max-w-6xl">
		<div use:reveal class="mb-16 text-center">
			<span class="font-hand text-terracotta text-2xl">together, we are</span>
			<h2 class="font-display text-ink mt-2 text-4xl font-bold md:text-6xl">Who We Are</h2>
		</div>

		<div class="who-grid">
			<!-- Main description card -->
			<div use:revealLeft class="who-card who-card-main">
				<p class="text-lg leading-relaxed md:text-xl">
					We are an intergenerational, global collective of educators, artists, youth, and
					imaginative minds — with a strong focus on the
					<span class="font-hand text-terracotta text-2xl">Global South</span>.
				</p>
				<p class="mt-4 text-lg leading-relaxed md:text-xl">
					We are <em>playful</em>, <em>curious</em>, <em>heart-led</em>,
					<em>polyvocal</em>, and a little bit
					<span class="font-hand text-magenta text-2xl">whacky</span>.
				</p>
			</div>

			<!-- Voice bubble 1 -->
			<div use:revealRight class="who-card who-card-voice who-card-1 delay-2">
				<p class="font-hand text-xl md:text-2xl">
					"We are not an institution. We are a living, breathing, co-created space."
				</p>
				<div class="mt-3 flex items-center gap-2">
					<div class="bg-teal h-2 w-2 rounded-full"></div>
					<span class="text-teal text-sm font-medium">collective voice</span>
				</div>
			</div>

			<!-- Voice bubble 2 -->
			<div use:reveal class="who-card who-card-voice who-card-2 delay-3">
				<p class="font-hand text-xl md:text-2xl">
					"We welcome all kinds of minds, including neurodivergent ones."
				</p>
				<div class="mt-3 flex items-center gap-2">
					<div class="bg-ochre h-2 w-2 rounded-full"></div>
					<span class="text-ochre text-sm font-medium">open invitation</span>
				</div>
			</div>

			<!-- Voice bubble 3 -->
			<div use:revealLeft class="who-card who-card-voice who-card-3 delay-4">
				<p class="font-hand text-xl md:text-2xl">
					"We hold liminality, uncertainty, and emergence with deep reverence for life."
				</p>
				<div class="mt-3 flex items-center gap-2">
					<div class="bg-magenta h-2 w-2 rounded-full"></div>
					<span class="text-magenta text-sm font-medium">our way</span>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- ===== WHAT WE BELIEVE ===== -->
<section id="beliefs" class="beliefs-section">
	<div class="mx-auto max-w-6xl px-6">
		<div use:reveal class="mb-16 text-center">
			<span class="font-hand text-paper/80 text-2xl">roots & wings</span>
			<h2 class="font-display text-paper mt-2 text-4xl font-bold md:text-6xl">
				What We Believe
			</h2>
		</div>

		<p use:reveal class="text-paper/90 mx-auto mb-16 max-w-3xl text-center text-lg md:text-xl">
			Reimagining schools means reimagining all of life as a place of learning — our
			relationships, our wounds, our gardens, our grandparents, our ancestors, our descendants.
		</p>

		<div class="beliefs-grid">
			{#each beliefs as belief, i (belief.text)}
				<div
					use:reveal
					class="belief-card delay-{(i % 6) + 1}"
					style="--rotation: {rotations[i]}deg"
				>
					<div class="belief-card-inner" style="background-color: {belief.color}">
						<p class="font-display text-paper text-lg font-semibold md:text-xl">
							{belief.text}
						</p>
					</div>
				</div>
			{/each}
		</div>

		<div use:reveal class="mt-20 text-center">
			<p class="font-hand text-ochre text-2xl md:text-3xl">
				It means transforming from the root: critically examining our ways of knowing, being,
				and relating — and reorienting them toward life, liberation, and equity.
			</p>
		</div>
	</div>
</section>

<!-- ===== VOICES & STORIES ===== -->
<section id="voices" class="relative px-6 py-24 md:py-36">
	<div class="mx-auto max-w-6xl">
		<div use:reveal class="mb-16 text-center">
			<span class="font-hand text-coral text-2xl">many voices, one pulse</span>
			<h2 class="font-display text-ink mt-2 text-4xl font-bold md:text-6xl">
				Voices & Stories
			</h2>
			<p class="text-ink/70 mt-4 text-lg">
				Stories from across the collective that bring reimagined learning to life
			</p>
		</div>

		<div class="voices-grid">
			{#each voices as voice, i (voice.author)}
				<div
					use:reveal
					class="voice-card voice-card-{voice.accent} delay-{(i % 4) + 1}"
					style="--rotation: {rotations[i]}deg"
				>
					<div class="voice-card-tape voice-tape-{voice.accent}"></div>
					<blockquote class="voice-quote">
						<p class="font-body text-ink text-lg italic leading-relaxed">
							"{voice.text}"
						</p>
					</blockquote>
					<div class="voice-meta">
						<p class="font-hand text-xl font-bold" style="color: {accentColors[voice.accent]}">
							{voice.author}
						</p>
						<p class="text-ink/50 text-sm">{voice.location}</p>
					</div>
				</div>
			{/each}
		</div>

		<div use:reveal class="mt-16 text-center">
			<p class="font-hand text-ink/60 text-xl">
				These are just a few of the many voices shaping our collective...
			</p>
		</div>
	</div>
</section>

<!-- ===== RESOURCES ===== -->
<section id="resources" class="resources-section">
	<div class="mx-auto max-w-6xl px-6">
		<div use:reveal class="mb-16 text-center">
			<span class="font-hand text-teal text-2xl">freely shared, always</span>
			<h2 class="font-display text-ink mt-2 text-4xl font-bold md:text-6xl">Resources</h2>
			<p class="text-ink/70 mt-4 text-lg">
				Creative outputs that communities and learning spaces can use and share freely. No
				paywalls. No barriers.
			</p>
		</div>

		<div class="resources-grid">
			{#each resources as resource, i (resource.title)}
				<div use:reveal class="resource-card delay-{(i % 3) + 1}">
					<div class="resource-icon resource-icon-{resource.color}">
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="1.5"
							stroke="currentColor"
							class="h-7 w-7"
						>
							<path stroke-linecap="round" stroke-linejoin="round" d={resource.icon} />
						</svg>
					</div>
					<h3 class="font-display text-ink mt-4 text-xl font-bold">{resource.title}</h3>
					<p class="text-ink/60 mt-2">{resource.desc}</p>
					<a
						href="#resources"
						class="font-hand mt-4 inline-block text-lg transition-transform hover:translate-x-1"
						style="color: {accentColors[resource.color]}"
					>
						explore &rarr;
					</a>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- ===== CONNECT ===== -->
<section id="connect" class="connect-section">
	<div class="mx-auto max-w-4xl px-6">
		<div use:reveal>
			<span class="font-hand text-ochre text-2xl">you belong here</span>
			<h2 class="font-display text-ink mt-2 text-4xl font-bold md:text-6xl">
				Share Your Story
			</h2>
		</div>

		<div use:reveal class="mt-8 max-w-2xl delay-2">
			<p class="text-ink/80 text-lg leading-relaxed md:text-xl">
				Every action — big or small — is relevant and welcome here. Whether you're a student
				dreaming of a different classroom, a teacher breaking the mold, an artist making the
				invisible visible, or a community member planting seeds of change.
			</p>
		</div>

		<div use:reveal class="connect-cta-grid delay-3">
			<div class="connect-card">
				<h3 class="font-display text-xl font-bold">Share a Story</h3>
				<p class="text-ink/60 mt-2">
					Tell us about a moment when learning came alive — in a garden, a conversation, a
					song, a struggle, a breakthrough.
				</p>
				<a href="mailto:hello@reimaginingschools.org" class="connect-button bg-terracotta">
					<span class="font-hand text-lg">Write to us</span>
				</a>
			</div>

			<div class="connect-card">
				<h3 class="font-display text-xl font-bold">Collaborate</h3>
				<p class="text-ink/60 mt-2">
					Something sparking your energy? Reach out. We love unexpected collaborations
					across borders, disciplines, and generations.
				</p>
				<a href="mailto:hello@reimaginingschools.org" class="connect-button bg-teal">
					<span class="font-hand text-lg">Let's connect</span>
				</a>
			</div>

			<div class="connect-card">
				<h3 class="font-display text-xl font-bold">Join the Collective</h3>
				<p class="text-ink/60 mt-2">
					There's no application, no gatekeeping. If this resonates, you're already one of
					us. Come as you are.
				</p>
				<a href="mailto:hello@reimaginingschools.org" class="connect-button bg-magenta">
					<span class="font-hand text-lg">Say hello</span>
				</a>
			</div>
		</div>

		<div use:reveal class="mt-16 text-center delay-4">
			<p class="font-hand text-ink/50 text-2xl md:text-3xl">
				"Leave inspired to take action toward an equitable, sustainable, imaginative future."
			</p>
		</div>
	</div>
</section>

<!-- ===== FOOTER ===== -->
<footer class="footer-section">
	<div class="mx-auto max-w-6xl px-6">
		<div class="footer-content">
			<div>
				<h3 class="font-display text-paper text-2xl font-bold">
					Reimagining Schools Collective
				</h3>
				<p class="font-hand text-paper/60 mt-2 text-xl">
					This space belongs to everyone.
				</p>
			</div>

			<div class="footer-links">
				<a href="#who-we-are" class="font-hand text-paper/70 text-lg hover:text-ochre transition-colors">Who We Are</a>
				<a href="#beliefs" class="font-hand text-paper/70 text-lg hover:text-ochre transition-colors">Beliefs</a>
				<a href="#voices" class="font-hand text-paper/70 text-lg hover:text-ochre transition-colors">Voices</a>
				<a href="#resources" class="font-hand text-paper/70 text-lg hover:text-ochre transition-colors">Resources</a>
				<a href="#connect" class="font-hand text-paper/70 text-lg hover:text-ochre transition-colors">Connect</a>
			</div>
		</div>

		<div class="border-paper/10 mt-12 border-t pt-8 text-center">
			<p class="text-paper/40 font-hand text-lg">
				Free and freely shared. No paywalls, no barriers, no hierarchy.
			</p>
			<p class="text-paper/30 mt-2 text-sm">
				Built with love by many hands &mdash; always growing, never finished.
			</p>
		</div>
	</div>
</footer>

<style>
	/* ===== HERO ===== */
	.hero-section {
		position: relative;
		min-height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		background: linear-gradient(
			145deg,
			var(--color-ink) 0%,
			#3d2f5c 25%,
			var(--color-terracotta) 55%,
			var(--color-ochre) 85%,
			var(--color-cream) 100%
		);
		overflow: hidden;
	}

	.hero-blob {
		position: absolute;
		border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
		opacity: 0;
		transition:
			opacity 1.5s ease-out,
			transform 1.5s cubic-bezier(0.16, 1, 0.3, 1);
		transform: scale(0.5);
	}

	.hero-blob.blob-animate {
		opacity: 1;
		transform: scale(1);
	}

	.blob-1 {
		width: 400px;
		height: 400px;
		background: radial-gradient(
			circle at 30% 30%,
			rgba(199, 91, 57, 0.35),
			rgba(199, 91, 57, 0.05)
		);
		top: -5%;
		right: -5%;
		animation: float-1 18s ease-in-out infinite;
		transition-delay: 0.2s;
	}

	.blob-2 {
		width: 300px;
		height: 300px;
		background: radial-gradient(
			circle at 70% 60%,
			rgba(26, 107, 90, 0.3),
			rgba(26, 107, 90, 0.05)
		);
		bottom: 10%;
		left: -3%;
		border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
		animation: float-2 22s ease-in-out infinite;
		transition-delay: 0.5s;
	}

	.blob-3 {
		width: 200px;
		height: 200px;
		background: radial-gradient(
			circle at 50% 50%,
			rgba(232, 168, 56, 0.3),
			rgba(232, 168, 56, 0.05)
		);
		top: 20%;
		left: 15%;
		border-radius: 30% 70% 60% 40% / 50% 40% 60% 50%;
		animation: float-3 15s ease-in-out infinite;
		transition-delay: 0.8s;
	}

	.blob-4 {
		width: 250px;
		height: 250px;
		background: radial-gradient(
			circle at 40% 40%,
			rgba(180, 75, 140, 0.2),
			rgba(180, 75, 140, 0.02)
		);
		bottom: 25%;
		right: 10%;
		border-radius: 50% 50% 40% 60% / 40% 60% 40% 60%;
		animation: float-1 20s ease-in-out infinite reverse;
		transition-delay: 1s;
	}

	.blob-5 {
		width: 150px;
		height: 150px;
		background: radial-gradient(
			circle at 60% 40%,
			rgba(135, 168, 120, 0.25),
			rgba(135, 168, 120, 0.02)
		);
		top: 50%;
		right: 25%;
		border-radius: 70% 30% 50% 50% / 30% 60% 40% 70%;
		animation: float-2 17s ease-in-out infinite;
		transition-delay: 1.2s;
	}

	.hero-scatter {
		position: absolute;
		font-family: var(--font-hand);
		color: rgba(254, 252, 247, 0.15);
		font-size: 4rem;
		opacity: 0;
		transition: opacity 2s ease-out;
		pointer-events: none;
	}

	.hero-scatter.scatter-animate {
		opacity: 1;
	}

	.scatter-1 {
		top: 15%;
		right: 20%;
		animation: float-1 12s ease-in-out infinite;
		font-size: 6rem;
	}

	.scatter-2 {
		bottom: 30%;
		left: 10%;
		animation: float-2 16s ease-in-out infinite;
		font-size: 5rem;
	}

	.scatter-3 {
		top: 60%;
		right: 8%;
		animation: float-3 14s ease-in-out infinite;
		font-size: 4rem;
	}

	.hero-content {
		position: relative;
		z-index: 10;
		text-align: center;
		padding: 2rem;
		opacity: 0;
		transform: translateY(30px);
		transition:
			opacity 1.2s cubic-bezier(0.16, 1, 0.3, 1),
			transform 1.2s cubic-bezier(0.16, 1, 0.3, 1);
		transition-delay: 0.3s;
	}

	.hero-content.hero-visible {
		opacity: 1;
		transform: translateY(0);
	}

	.hero-kicker {
		color: var(--color-ochre);
		font-size: 1.5rem;
		margin-bottom: 1rem;
		letter-spacing: 0.02em;
	}

	.hero-title {
		color: var(--color-paper);
		font-size: clamp(2.8rem, 8vw, 7rem);
		line-height: 0.95;
		font-weight: 900;
		letter-spacing: -0.02em;
	}

	.hero-title-line {
		display: block;
	}

	.hero-title-accent {
		color: var(--color-ochre);
		font-style: italic;
		transform: rotate(-1deg);
		display: inline-block;
	}

	.hero-subtitle {
		color: rgba(254, 252, 247, 0.8);
		font-size: clamp(1rem, 2vw, 1.3rem);
		margin-top: 1.5rem;
		max-width: 600px;
		margin-inline: auto;
		line-height: 1.6;
	}

	.hero-whisper {
		color: var(--color-coral);
		font-size: 1.6rem;
		margin-top: 2rem;
		animation: pulse-soft 4s ease-in-out infinite;
	}

	.scroll-indicator {
		position: absolute;
		bottom: 2rem;
		left: 50%;
		transform: translateX(-50%);
		opacity: 0;
		transition: opacity 1.5s ease-out;
		transition-delay: 2s;
	}

	.scroll-indicator.scroll-visible {
		opacity: 1;
	}

	.scroll-line {
		width: 2px;
		height: 40px;
		background: linear-gradient(to bottom, rgba(254, 252, 247, 0.5), transparent);
		animation: scroll-hint 2s ease-in-out infinite;
	}

	/* ===== WHO WE ARE ===== */
	.section-wave {
		position: absolute;
		top: -2px;
		left: 0;
		right: 0;
		color: var(--color-ink);
		line-height: 0;
	}

	.section-wave svg {
		width: 100%;
		height: 60px;
	}

	.who-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 1.5rem;
	}

	@media (min-width: 768px) {
		.who-grid {
			grid-template-columns: 1.2fr 1fr;
			gap: 2rem;
		}
	}

	.who-card {
		padding: 2rem;
		border-radius: 4px;
		position: relative;
	}

	.who-card-main {
		background: var(--color-paper);
		box-shadow:
			4px 4px 0 var(--color-terracotta),
			8px 8px 0 rgba(199, 91, 57, 0.15);
		grid-row: 1;
	}

	@media (min-width: 768px) {
		.who-card-main {
			grid-row: 1 / 3;
		}
	}

	.who-card-voice {
		background: var(--color-paper);
		border-left: 4px solid;
		animation: sway 6s ease-in-out infinite;
	}

	.who-card-1 {
		border-color: var(--color-teal);
		--rotation: -1deg;
		transform: rotate(-1deg);
	}

	.who-card-2 {
		border-color: var(--color-ochre);
		--rotation: 1.5deg;
		transform: rotate(1.5deg);
	}

	.who-card-3 {
		border-color: var(--color-magenta);
		--rotation: -0.5deg;
		transform: rotate(-0.5deg);
	}

	@media (min-width: 768px) {
		.who-card-3 {
			grid-column: 1 / -1;
			max-width: 500px;
			margin-left: auto;
		}
	}

	/* ===== BELIEFS ===== */
	.beliefs-section {
		background: var(--color-ink);
		padding: 6rem 0;
		position: relative;
		overflow: hidden;
	}

	@media (min-width: 768px) {
		.beliefs-section {
			padding: 9rem 0;
		}
	}

	.beliefs-section::before {
		content: '';
		position: absolute;
		inset: 0;
		background: radial-gradient(
				ellipse at 20% 50%,
				rgba(199, 91, 57, 0.15),
				transparent 60%
			),
			radial-gradient(ellipse at 80% 30%, rgba(26, 107, 90, 0.1), transparent 50%),
			radial-gradient(ellipse at 50% 80%, rgba(180, 75, 140, 0.08), transparent 40%);
	}

	.beliefs-section > * {
		position: relative;
	}

	.beliefs-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
		gap: 1.5rem;
	}

	@media (min-width: 768px) {
		.beliefs-grid {
			grid-template-columns: repeat(3, 1fr);
			gap: 2rem;
		}
	}

	.belief-card {
		transform: rotate(var(--rotation, 0deg));
		transition: transform 0.3s ease;
	}

	.belief-card:hover {
		transform: rotate(0deg) scale(1.04);
	}

	.belief-card-inner {
		padding: 2rem;
		border-radius: 3px;
		min-height: 130px;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		box-shadow: 4px 4px 20px rgba(0, 0, 0, 0.3);
	}

	/* ===== VOICES ===== */
	.voices-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 2rem;
	}

	@media (min-width: 640px) {
		.voices-grid {
			grid-template-columns: repeat(2, 1fr);
		}
	}

	@media (min-width: 1024px) {
		.voices-grid {
			grid-template-columns: repeat(3, 1fr);
		}
	}

	.voice-card {
		background: var(--color-paper);
		padding: 2rem;
		padding-top: 2.5rem;
		border-radius: 2px;
		position: relative;
		transform: rotate(var(--rotation, 0deg));
		transition:
			transform 0.4s cubic-bezier(0.16, 1, 0.3, 1),
			box-shadow 0.4s ease;
		box-shadow: 2px 2px 15px rgba(43, 45, 66, 0.08);
	}

	.voice-card:hover {
		transform: rotate(0deg) translateY(-4px);
		box-shadow: 4px 8px 25px rgba(43, 45, 66, 0.15);
	}

	.voice-card-tape {
		position: absolute;
		top: -8px;
		left: 50%;
		transform: translateX(-50%) rotate(var(--rotation, 0deg));
		width: 55px;
		height: 20px;
		border-radius: 1px;
		opacity: 0.6;
	}

	.voice-tape-terracotta {
		background: linear-gradient(135deg, rgba(199, 91, 57, 0.5), rgba(199, 91, 57, 0.3));
	}
	.voice-tape-teal {
		background: linear-gradient(135deg, rgba(26, 107, 90, 0.5), rgba(26, 107, 90, 0.3));
	}
	.voice-tape-magenta {
		background: linear-gradient(135deg, rgba(180, 75, 140, 0.5), rgba(180, 75, 140, 0.3));
	}
	.voice-tape-ochre {
		background: linear-gradient(135deg, rgba(232, 168, 56, 0.5), rgba(232, 168, 56, 0.3));
	}
	.voice-tape-coral {
		background: linear-gradient(135deg, rgba(232, 116, 97, 0.5), rgba(232, 116, 97, 0.3));
	}
	.voice-tape-sage {
		background: linear-gradient(135deg, rgba(135, 168, 120, 0.5), rgba(135, 168, 120, 0.3));
	}

	.voice-card-terracotta {
		border-bottom: 3px solid var(--color-terracotta);
	}
	.voice-card-teal {
		border-bottom: 3px solid var(--color-teal);
	}
	.voice-card-magenta {
		border-bottom: 3px solid var(--color-magenta);
	}
	.voice-card-ochre {
		border-bottom: 3px solid var(--color-ochre);
	}
	.voice-card-coral {
		border-bottom: 3px solid var(--color-coral);
	}
	.voice-card-sage {
		border-bottom: 3px solid var(--color-sage);
	}

	.voice-quote {
		margin-bottom: 1rem;
	}

	.voice-meta {
		padding-top: 1rem;
		border-top: 1px solid rgba(43, 45, 66, 0.08);
	}

	/* ===== RESOURCES ===== */
	.resources-section {
		background: linear-gradient(180deg, var(--color-cream) 0%, var(--color-paper) 100%);
		padding: 6rem 0;
	}

	@media (min-width: 768px) {
		.resources-section {
			padding: 9rem 0;
		}
	}

	.resources-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 1.5rem;
	}

	@media (min-width: 640px) {
		.resources-grid {
			grid-template-columns: repeat(2, 1fr);
		}
	}

	@media (min-width: 1024px) {
		.resources-grid {
			grid-template-columns: repeat(3, 1fr);
		}
	}

	.resource-card {
		background: var(--color-paper);
		padding: 2rem;
		border-radius: 4px;
		border: 1px solid rgba(43, 45, 66, 0.06);
		transition:
			transform 0.3s ease,
			box-shadow 0.3s ease;
		position: relative;
		overflow: hidden;
	}

	.resource-card::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 3px;
	}

	.resource-card:hover {
		transform: translateY(-3px);
		box-shadow: 0 8px 25px rgba(43, 45, 66, 0.1);
	}

	.resource-icon {
		width: 48px;
		height: 48px;
		border-radius: 12px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.resource-icon-magenta {
		background: rgba(180, 75, 140, 0.12);
		color: var(--color-magenta);
	}
	.resource-icon-terracotta {
		background: rgba(199, 91, 57, 0.12);
		color: var(--color-terracotta);
	}
	.resource-icon-teal {
		background: rgba(26, 107, 90, 0.12);
		color: var(--color-teal);
	}
	.resource-icon-ochre {
		background: rgba(232, 168, 56, 0.12);
		color: var(--color-ochre);
	}
	.resource-icon-sage {
		background: rgba(135, 168, 120, 0.12);
		color: var(--color-sage);
	}
	.resource-icon-coral {
		background: rgba(232, 116, 97, 0.12);
		color: var(--color-coral);
	}

	/* ===== CONNECT ===== */
	.connect-section {
		padding: 6rem 0;
		background: var(--color-cream);
		position: relative;
	}

	@media (min-width: 768px) {
		.connect-section {
			padding: 9rem 0;
		}
	}

	.connect-section::before {
		content: '';
		position: absolute;
		top: 0;
		left: 5%;
		right: 5%;
		height: 1px;
		background: linear-gradient(
			90deg,
			transparent,
			var(--color-terracotta),
			var(--color-ochre),
			var(--color-teal),
			transparent
		);
	}

	.connect-cta-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 1.5rem;
		margin-top: 2.5rem;
	}

	@media (min-width: 768px) {
		.connect-cta-grid {
			grid-template-columns: repeat(3, 1fr);
		}
	}

	.connect-card {
		background: var(--color-paper);
		padding: 2rem;
		border-radius: 4px;
		box-shadow: 2px 2px 10px rgba(43, 45, 66, 0.06);
		display: flex;
		flex-direction: column;
	}

	.connect-button {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: 0.75rem 1.5rem;
		border-radius: 3px;
		color: var(--color-paper);
		margin-top: auto;
		margin-top: 1.5rem;
		transition:
			transform 0.2s ease,
			box-shadow 0.2s ease;
		text-decoration: none;
	}

	.connect-button:hover {
		transform: translateY(-2px);
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
	}

	/* ===== FOOTER ===== */
	.footer-section {
		background: var(--color-ink);
		padding: 4rem 0;
		position: relative;
	}

	.footer-section::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 4px;
		background: linear-gradient(
			90deg,
			var(--color-terracotta),
			var(--color-ochre),
			var(--color-teal),
			var(--color-magenta),
			var(--color-coral),
			var(--color-sage)
		);
	}

	.footer-content {
		display: flex;
		flex-direction: column;
		gap: 2rem;
	}

	@media (min-width: 768px) {
		.footer-content {
			flex-direction: row;
			justify-content: space-between;
			align-items: flex-start;
		}
	}

	.footer-links {
		display: flex;
		flex-wrap: wrap;
		gap: 1.5rem;
	}
</style>
