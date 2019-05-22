<template>
	<div class="notes-app">
		<notes-header :title="title" />
		<notes-editor @createNote="createNoteHandler" @saveChanges="saveNote" ref="edit"/>
		<notes-grid :notes="notes"  @deleteNote="deleteNoteHandler" @editNote="editNoteHandler" />
	</div>
</template>

<script>
	import NotesHeader from '@/components/NotesHeader.vue';
	import NotesEditor from '@/components/NotesEditor.vue';
	import NotesGrid from '@/components/NotesGrid.vue';

	const notes = localStorage.notes ? JSON.parse(localStorage.notes) : [];

	export default {
		name: 'notes-app',
		components: {
			NotesHeader,
			NotesEditor,
			NotesGrid,
		},

		data: () => ({
			title: 'Tetiana Movlian Notes App',
			notes,
		}),

		methods: {
			createNoteHandler(note) {
				this.notes.push(note)
      			localStorage.notes = JSON.stringify(notes)  				
				// console.log("Push new note in App");				
			},
			saveNote(note) {
				this.notes = this.notes.map((item) => item.id === note.id ? note : item);
				localStorage.notes = JSON.stringify(this.notes);
				// console.log("Save edit note in App");
    		},
			deleteNoteHandler(id) {				
				this.notes = this.notes.filter(note => note.id !== id);
				localStorage.notes = JSON.stringify(this.notes);				
				// console.log("Delete note in App");
			},
			editNoteHandler(note){
				this.$refs.edit.setEdit(note);
				// console.log("Edit in App");
			}
		},
	};
</script>

<style lang="scss">
	$color: #eaeaea;

	* {
		box-sizing: border-box;
	}

	body {
		font-family: sans-serif;
		font-weight: 300;
		background-color: $color;
	}

	.notes-app {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
		max-width: 980px;
		margin: 0 auto;
	}
</style>
