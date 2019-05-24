<template>
	<div class="note-editor">
		<textarea v-model="text" placeholder="Enter your note here ..." rows="5" />
		
		<div class="d-flex justify-content-between">
			<div class='color-picker'>				
				<input type = "color" v-if="!isEditing" v-model='bgColorDefault'>
				<input type = "color" v-if="isEditing" v-model='bgColor'>
			</div>
			<div class="d-flex justify-content-flex-end">
			<button
				class="add-button"
				@click="addOrEditNote"
				:disabled="text.trim().length === 0"
			>{{ isEditing ? "Save" : "Add"}}				
			</button>
			<button v-show="isEditing" @click="cancelEdit" class="cancel-button">Cancel</button>
			
		</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'notes-editor',
		data: () => ({
			text: '',
			bgColorDefault:'#44c767',
			bgColor: '#44c767' ,
			isEditing: null,
		}),

		methods: {
			addOrEditNote() {
				if (this.isEditing){							
					this.editNote();
				}
				else{
					const note = {
						id: new Date().getTime(),
						text: this.text,
						bgcolor: this.bgColorDefault
					};
					// this.$parent.notes.push(note);
					this.$emit('createNote', note);					
					this.text = '';
				}
			},
			setEdit(note) {
				this.bgColor = note.bgcolor;
				this.isEditing = note;
				this.text = note.text;
			},
			editNote(){				
				const note = {
					...this.isEditing,
					text: this.text,
					bgcolor: this.bgColor
				};
				
				this.$emit("saveChanges", note);
				this.isEditing = null;
				this.text = "";
			},			
			cancelEdit() {
				this.isEditing = null;
      			this.text = "";
				// console.log("Cancel Edit");
			}
		}
	};
</script>

<style lang="scss" scoped>
	.note-editor {
		width: 100%;
		max-width: 600px;
		padding: 16px;
		margin: 16px auto;
		background-color: white;
		box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
		border-radius: 2px;
		display: flex;
		flex-direction: column;
	}

	textarea {
		width: 100%;
		resize: none;
		margin: 5px;
		font-size: 14px;
		border: none;
		font-weight: 300;		
	}

	textarea:focus {
		outline: 0;
	}

	input {	
		margin-top: 15px;
		cursor: pointer;				
	}
	
	.add-button {
		width: 100px;
		background-color: #44c767;
		border-radius: 8px;
		border: 1px solid #18ab29;
		cursor: pointer;
		color: #ffffff;
		font-size: 14px;
		padding: 8px 8px;
		margin-right: 8px;
		text-transform: uppercase;
		text-decoration: none;
		text-shadow: 0px 1px 0px #2f6627;
	}

	.add-button:hover {
		background-color: #5cbf2a;
	}

	.add-button:active {
		position: relative;
		top: 1px;
	}

	.add-button:focus {
		outline: 0;
	}

	.cancel-button {
		width: 100px;
		background-color: #d82f2f;
		border-radius: 8px;
		border: 1px solid #ff0001;
		cursor: pointer;
		color: #ffffff;
		font-size: 14px;
		padding: 8px 8px;
		text-transform: uppercase;
		text-decoration: none;
		text-shadow: 0px 1px 0px #662727;
	}

	.cancel-button:hover {
		background-color: #f70000;
	}

	.cancel-button:active {
		position: relative;
		top: 1px;
	}

	.cancel-button:focus {
		outline: 0;
	}
</style>
