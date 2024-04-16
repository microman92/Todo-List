<template>
  <div class="wrapper">
    <Navbar @setSearch="searchValue = $event" />

    <Notes :notes="filterNotes" @delNote="delNote" @change="change" />
    <Modal @close="isModalOpen = false" v-show="isModalOpen" @addNote="addNote" :edit="edit" :editedNote="editedNote"
      @changedNote="changedNote" />

    <button class="add__note" @click="; (isModalOpen = true), (edit = false)" v-if="!isModalOpen">
      <img src="@/assets/img/pens.svg" alt="" />
    </button>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Notes from '@/components/Notes.vue'
import Modal from './components/Modal.vue'

export default {
  components: {
    Navbar,
    Notes,
    Modal,
  },

  data() {
    return {
      isModalOpen: false,
      edit: false,
      searchValue: '',
      editedNote: null,
      notes: [],
    }
  },
  methods: {
    addNote(note) {
      this.notes.push(note)
    },
    delNote(id) {
      this.notes.splice(id, 1)
    },

    getNotes() {
      let localNotes = localStorage.notes
      if (localNotes) {
        this.notes = JSON.parse(localNotes)
      }
    },

    change(id) {
      this.isModalOpen = this.edit = true
      let currentNote = this.notes.find((note) => note.id == id)
      console.log(currentNote)
      this.editedNote = currentNote
    },

    changedNote(newNote) {
      this.notes.forEach((note) => {
        if (note.id == newNote.id) {
          note.title = newNote.title
          note.text = newNote.text
          note.date = newNote.date
        }
      })
    },
  },

  computed: {
    filterNotes() {
      return this.searchValue
        ? this.notes.filter((note) =>
          note.title.toLowerCase().includes(this.searchValue.toLowerCase())
        )
        : this.notes
    },
  },

  mounted() {
    this.getNotes()
    console.log(this.close)
  },

  watch: {
    notes: {
      handler() {
        localStorage.notes = JSON.stringify(this.notes)
      },
      deep: true,
    },
  },
}
</script>
