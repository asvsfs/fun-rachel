<script lang="ts">
	import { onMount } from 'svelte';
	import { elasticOut, linear } from 'svelte/easing';
	import { fade, fly, scale } from 'svelte/transition';
	import Typewriter from 'svelte-typewriter';
	let animations: { [key: string]: boolean } = {};
	animations['hello'] = false;
	animations['welcome'] = false;
	animations['rachel_img'] = false;
	animations['explaination'] = false;
	animations['amir_img'] = false;
	animations['question_1'] = false;
	onMount(() => {
		animations['hello'] = true;
	});
</script>

<div class="w-full h-full justify-center items-center flex flex-col">
	{#if animations['hello']}
		<Typewriter
			interval={50}
			on:done={() => {
				setTimeout(() => {
					animations['rachel_img'] = true;
					setTimeout(() => {
						animations['rachel_img'] = false;
						animations['amir_img'] = true;
					}, 1000);
				}, 500);
			}}
		>
			<p class="justify-center flex text-2xl">Hello Rachel, Good Day</p>
		</Typewriter>
	{/if}
	<div class="relative w-full flex justify-center items-center h-[400px] overflow-hidden">
		{#if animations['rachel_img']}
			<img
				class="flex absolute"
				in:fly={{ duration: 500, x: -200, easing: elasticOut }}
				out:fly={{ duration: 500, x: 500, easing: linear }}
				src="/rachel.png"
				width="300px"
			/>
		{/if}

		{#if animations['amir_img']}
			<img
				class="flex absolute"
				in:fly={{ duration: 500, x: -500, easing: linear, opacity: 1 }}
				on:introend={() => {
					animations['question_1'] = true;
				}}
				src="/amir2.png"
				width="300px"
			/>
		{/if}
	</div>
	{#if animations['question_1']}
		<Typewriter
			interval={50}
			on:done={() => {
				setTimeout(() => {
					animations['question_1'] = false;
					animations['amir_img'] = false;
					animations['hello'] = false;
					animations['why_u_so_bitchy'] = true;
				}, 2000);
			}}
		>
			<p class="justify-center flex text-2xl">I got a question</p>
		</Typewriter>
	{/if}
	{#if animations['why_u_so_bitchy']}
		<p
			on:introend={() => {
				setTimeout(() => {
					animations['huh'] = true;
				}, 300);
			}}
			in:scale={{ duration: 200 }}
			class="tilted"
		>
			Why You So Bitchy?
		</p>
	{/if}
	{#if animations['huh']}
		<Typewriter on:done={()=>{
      
        }}>
			<p class="tilted">Huh?</p>
		</Typewriter>
	{/if}
 
</div>

<style>
	.tilted {
		font-size: 3rem;
		transform: rotate(-5deg);
	}
</style>
