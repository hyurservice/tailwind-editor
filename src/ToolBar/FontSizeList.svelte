<script>

	import DropDown from './DropDown.svelte'
	import DownIcon from '../Icons/DownIcon.svelte'
	
	export let setClass
	export let klass  = ''

	let list = [
		{
			label:'Small',
			value:'md:text-sm text-sm'
		},
		{
			label:'Normal',
			value:'md:text-base text-base'
		},
		{
			label:'Large',
			value:'md:text-xl text-lg'
		},
		{
			label:'Extra Large',
			value:'md:text-3xl text-xl'
		},
		{
			label:'Huge',
			value:'md:text-6xl text-4xl'
		},
	]


	function inList(){
		let lastFoundPos = -1;
		let lastFound = false;
		for (let v of list) {
			const pos = klass.indexOf(v.value);
			if (pos >= 0 && pos > lastFoundPos) {
				lastFound = v.value;
				lastFoundPos = pos;
			}
		}
		return lastFound;
	}

	$: text_class = inList() || ''
	$: selected_val = text_class

	
	$: selected = list.find(e => e.value==selected_val)
	$: selected_label = (selected&&selected.label)||'Normal'

	

	let open = false
	function selectClass(evt){
		selected_val = evt.detail
		open = false
		setClass(evt.detail)
	}
</script>

<div class="flex h-full">
	<DropDown {list} bind:open={open} selected={selected_val} on:select={selectClass} class="w-32 text-sm">
		<div class="pl-2 pr-3 py-1 h-full flex items-center whitespace-nowrap flex-shrink-0">
			{selected_label} <DownIcon />
		</div>
	</DropDown>
</div>