<script>
	import '../app.css';
	import { Footer, CTAs, Header } from '../components';
	import { openModal } from '../store';
	import { onMount, onDestroy } from 'svelte';

	let viewportwidth;
	let y;
	$: outerHeight = 0;

	function reroute(href) {
		$openModal = false;
		window.location.href = href;
	}

	function updateViewportSize() {
		if (typeof window !== 'undefined') {
			viewportwidth = window.innerWidth;
			if (viewportwidth > 768) $openModal = false;
		}
	}

	onMount(() => {
		updateViewportSize();
		if (typeof window !== 'undefined') window.addEventListener('resize', updateViewportSize);
	});

	onDestroy(() => {
		if (typeof window !== 'undefined') window.removeEventListener('resize', updateViewportSize);
	});
</script>

{#if $openModal}
	<div
		class={`fixed top-0 left-0 w-screen h-screen border-b bg-white z-50 flex flex-col gap-8 p-5 px-8 md:hidden ${openModal ? '' : 'hidden'}`}
	>
		<div class="flex items-center justify-between gap-4 border-b pb-2">
			<h1 class="font-semibold">Swoley <span class="text-indigo-400">Moley</span></h1>
			<button on:click={() => ($openModal = false)} class="outline-none border-none">
				<i class="fa-solid fa-xmark text-2xl" />
			</button>
		</div>
		<div class="flex flex-col gap-4 flex-1">
			<button
				on:click={() => reroute('#product')}
				class="border-none outline-none p-2 group duration-200 cursor-pointer text-left"
			>
				<p class="duration-200 group-hover:pl-2 font-poppins text-3xl font-semibold">
					Product <i class="fa-solid fa-chevron-right text-xl p-4" />
				</p>
			</button>
			<button
				on:click={() => reroute('#reviews')}
				class="border-none outline-none p-2 group duration-200 cursor-pointer text-left"
			>
				<p class="duration-200 group-hover:pl-2 font-poppins text-3xl font-semibold">
					Reviews <i class="fa-solid fa-chevron-right text-xl p-4" />
				</p>
			</button>
			<button
				on:click={() => reroute('#faqs')}
				class="border-none outline-none p-2 group duration-200 cursor-pointer text-left"
			>
				<p class="duration-200 group-hover:pl-2 font-poppins text-3xl font-semibold">
					FAQs <i class="fa-solid fa-chevron-right text-xl p-4" />
				</p>
			</button>
		</div>
		<div class="flex flex-col items-center justify-center">
			<CTAs />
		</div>
	</div>
{/if}

{#if y > outerHeight}
	<div class="bg-white fixed top-0 left-0 w-full flex flex-col z-20 px-4 fadeIn">
		<Header />
	</div>
{/if}

<slot />
<Footer />
<svelte:window bind:scrollY={y} bind:outerHeight />
<!-- 
header
hero
product description
user reviews
faq
conversion
footer
 -->
