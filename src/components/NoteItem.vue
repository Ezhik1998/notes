<template>
	<div>
		<div class="note" :style="{ backgroundColor: note.bgcolor }">		
			<div class="edit-delete">
				<div class="edit-note"  @click="editing" >
					<i class="material-icons">edit</i>	
				</div>		
				<div class="delete-note" @click="$emit('deleteNote', note.id)">
					<i class="material-icons">
						delete
					</i>
				</div>
			</div>		
			<span>{{ note.text }}</span>		
		</div>	
	</div>
</template>

<script>
	export default {
		name: 'note-item',
		props: {
			note: {
				type: Object,
				required: true,
			},
		},	
		methods: {
			editing(note) {
				this.$emit("editNote", this.note);
				// console.log("Edit in Item");
   		},
		}
};
</script>

<style lang="scss" scoped>
	.note {
		width: 200px;
		height: auto;
		float: left;
		box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
		border-radius: 2px;
		padding: 10px;
		margin-bottom: 10px;
		transition: box-shadow 0.3s;
		word-wrap: break-word;
		position: relative;
	}

	.note:hover {
		box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
	}

	.edit-delete{		
		display: flex;
  	justify-content: flex-end;		  
	}
	.delete-note {
		top: 5px;
		right: 5px;
		color: rgba(0, 0, 0, 0.6);
		cursor: pointer;
	}
	.edit-note {
		top: 5px;
		right: 5px;
		color: rgba(0, 0, 0, 0.6);
		cursor: pointer;
	}
	.material-icons {
		font-family: 'Material Icons';
		font-weight: normal;
		font-style: normal;
		font-size: 18px;  
		display: inline-block;	
	}
</style>
