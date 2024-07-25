<script>
	export let dark;
</script>

<div class="flex items-center gap-4">
	<button class={'transition duration-300 ease-in-out specialBtn ' + (dark ? 'bg-[#181b34]' : '')}>
		<p class="text-base sm:text-lg">Contact Us</p>
	</button>
	<button class="specialBtnDark px-6 transition duration-300 ease-in-out hover:bg-blue-800">
		<p class="text-base sm:text-lg">Get Started &rarr;</p>
	</button>
</div>
