<script>
	import Dashboard from "./components/Dashboard.svelte";
	import Header from "./components/Header.svelte";

	import {v4} from 'uuid';


	let notes = [
	{
		id: 0,
		title: 'Vacaciones',
		color: 'peru',
		text: 'Hola!'
	}
];

let copyNotes = [...notes];
$: count = notes.length;

function handleNew() {
	const color = generateColor();
	const note = {
		id: v4(),   /*--uuid nos genera un codigo unico p/cada note*/
		title:'',
		color: color,
		text:''
	};
	notes = [note, ...notes];
	copyNotes = [...notes];
}

function generateColor() { /*Elijo de forma aleatoria del arreglo*/
	const colors = ['#DDFFC2', '#FFC2C2', '#FFEAC2', '#C2FFD3', '#C2FFEC', '#C2FAFF', '#C2E2FF', '#CBC2FF', '#EBC2FF', '#FFC2F7', '#FFC2D8'];
	const index = Math.floor(Math.random() * (colors.length));
	return colors[index];
	
}

function handleUpdate(e) {   
	const note = e.detail;
	const index = notes.findIndex(note => note.id === e.detail.id);
	notes[index] = e.detail;
		
}


function handleColor(event){
		const id = event.detail.id;
		const index = notes.findIndex(note => note.id === id);
		notes[index].color = generateColor();
		copyNotes[index].color = generateColor()
}


function handleRemove(e) {
	const response = notes.filter(n => n.id != e.detail.id);
	notes = [...response];
	copyNotes = [...notes];
}

function handleSearch(e) {
	const q = e.target.value;

	if (q=='') {
		copyNotes = [...notes];
		return false;
	}

	const results = notes.filter(note => {
		const title = note.title.toLocaleLowerCase();
		const text = note.text.toLocaleLowerCase();

		return title.indexOf(q) > -1 || text.indexOf(q) > -1;
	});
	copyNotes = [... results];
	
}

</script>



<main>
	<Header on:input={handleSearch}/>
	<div class="count-notes"> 
		<b>	{count} notas </b>
	</div>
	
	<Dashboard 
		bind:notes = {copyNotes} 
		on:click = {handleNew} 
		on:update = {handleUpdate}
		on:color = {handleColor}
		on:remove={handleRemove} />

</main>


<style>
	:global(body){
		background-color:transparent;
		font-family: 'Courier New', Courier, monospace;
	}

	.count-notes{
		padding: 20px 20px 0 20px;
		text-align: right;
		color: cornflowerblue;
		font-size: 16px;
	}

	
</style>