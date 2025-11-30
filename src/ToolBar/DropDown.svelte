<script>
    import {onMount} from 'svelte'

	import List from './List.svelte'
	let klass = ''
	export let open = false
	export {klass as class}
	export let selected

	$: posKlass = lNode?.getBoundingClientRect()?.bottom > window.innerHeight ? 'bottom-0 mb-8' : ''

	let lNode


	export let list = [
		{
			label:'none',
			value:'none'
		},
		{
			label:'tight',
			value:'tight'
		},
		{
			label:'snug',
			value:'snug'
		},
		{
			label:'normal',
			value:'normal'
		},
		{
			label:'relaxed',
			value:'relaxed'
		},
		{
			label:'loose',
			value:'loose'
		}
	]

	function toggleList(e){
		open= !open
		e.preventDefault()
		e.stopPropagation()
	}

	function hideList(){
		open = false
	}

    onMount(() => {
        window.addEventListener('click', hideList)

        return () => {
            window.removeEventListener('click', hideList);
        };
    })
</script>

<div class="se-dropdown relative">
	<div class="cursor-pointer flex h-full" on:click={toggleList}>
		<slot>Click To show</slot>
	</div>
	{#if open}
	<div class="absolute -ml-1 z-920 z-20 {klass} {posKlass}" bind:this={lNode}>
		<List {list} {selected} on:select />
	</div>
	{/if}
</div>
