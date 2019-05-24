<template>
    <div class="notes-grid" ref="grid">
        <NoteItem
            v-for="note in notes"            
            :key="note.id"
            :note="note"
			@deleteNote="$emit('deleteNote', note.id)"
        	@editNote="$emit('editNote', note)"
        />
    </div>
</template>

<script>
import NoteItem from '@/components/NoteItem.vue'
import Masonry from 'masonry-layout'

export default {
    name: 'notes-grid',
    components: {
        NoteItem,
    },
    props: {
        notes: {
            type: Array,
            required: true
        }
	},	
    mounted() {
        const grid = this.$refs.grid
        this.msnry = new Masonry(grid, {
            itemSelector: '.note',
            columnWidth: 200,
            gutter: 10,
            isFitWidth: true,
        })
    },
    updated() {
        this.msnry.reloadItems()
        this.msnry.layout()
    }
}
</script>

<style>
.notes-grid {
    margin: 0 auto;
}
</style>
