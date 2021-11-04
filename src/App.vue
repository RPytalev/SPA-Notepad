<template>
  <div class="container">
    <div class="header"><h1>App</h1></div>
    <div class="main">
      <div>
        <NotesListDisplay :selectedNote="selectedNote" :notesList="notesList" @note-selected="noteSelected" @switch-reminder="switchReminder" @delete-note="deleteNote" />
      </div>
      <div>
        <NoteEditorDisplay :tagsList="tagsList" :note="note" :showNewTextarea="showNewTextarea" @create-note="createNote" @create-new-note="createNewNote" @create-new-textarea="createNewTextarea" />
      </div>
    </div>
    <div class="footer"></div>
  </div>
</template>

<script>
  import NotesListDisplay from './components/NotesListDisplay.vue'
  import NoteEditorDisplay from './components/NoteEditorDisplay.vue'

  export default {
    name: "App",
    components: {
      NotesListDisplay,
      NoteEditorDisplay
    },
    methods: {
      createNote(noteNew, tagsNew) {
        this.notesList = [...this.notesList, noteNew];
        document.querySelector('#textarea').value = '';
        this.notesList = this.notesList.filter(( item ) => item.id !== this.selectedNote);
        
        for (var i = 0; i < tagsNew.length; i++) {

	        if(this.tagsList.includes(tagsNew[i], 0)) {
	        	return;
	        } 	
	          this.tagsList.push(tagsNew[i]);
            this.selectedNote = 0;
        } 
      },
      createNewTextarea() {
        this.showNewTextarea = true;
        document.querySelector('#new-textarea').value = '';
      },
      createNewNote(newNote, newTags) {
        this.notesList = [...this.notesList, newNote];
        this.showNewTextarea = false;
        
        for (var i = 0; i < newTags.length; i++) {

	        if(this.tagsList.includes(newTags[i], 0)) {
	        	return;
	        } 	
	          this.tagsList.push(newTags[i]);
            this.selectedNote = 0;
        }
      },
      switchReminder(id) {
        this.notesList = this.notesList.map((item) => item.id == id ? {...item, reminder: !item.reminder} : item)
      },
      deleteNote() {
            this.notesList = this.notesList.filter(( item ) => item.id !== this.selectedNote);
            document.querySelector('#textarea').value = '';
            this.selectedNote = 0;
            console.log(this.note.text);
            let selectedNoteTags = this.note.text.match(/#[a-z A-Z 0-9]+/g);
            console.log(selectedNoteTags);
      },
      noteSelected(id) {
        this.note = this.notesList.filter(( item ) => item.id == id)[0];
        this.selectedNote = id;
      },
      findTag() {
        let arr = this.notesList.map(( item )=> item = item.text);
        let str = String(arr);
        let arrTags = str.match(/#[a-z A-Z 0-9]+/g);
        this.tagsList = this.tagsList.concat(arrTags);
        return this.tagsList;
      }
    },
  data() {
    return {
      notesList: [
        {
          id: 1,
          text: 'Meeting with Nik #meeting',
          date: 'November 1st 22:00 pm',
          reminder: false
        },
        {
          id: 2,
          text: 'Shopping with wife #shopping',
          date: 'December 2nd 15:00 pm',
          reminder: false
        },
        {
          id: 3,
          text: 'Nikita\'s party #party',
          date: 'December 3rd 7:00 am',
          reminder: false
        },
        {
          id: 4,
          text: 'Vacation start',
          date: 'July 15th 00:01 am',
          reminder: false
        }
      ],
      selectedNote: 0,
      note: {},
      showNewTextarea: false,
      tagsList: [],
      noteTags: []
    }
  }
}
</script>

<style lang="sass">
$primary-color: #ff7800
$primary-background-color: rgba(0,0,0, .9)

html 
  margin: 0
  padding: 0

.container
  box-sizing: border-box
  width: 1200px
  height: 80vh
  margin: 0 auto
  padding: 0
  background-color: $primary-background-color
  color: $primary-color
  text-align: center

  .header 
    width: 100%
    height: 4rem
    background-color: green
    color: #fff
  
  .main
    display: flex
    justify-content: space-around
    width: 100%
    height: 60vh
    background-color: #000
    color: #000

  .footer
    width: 100%
    height: 4rem
    background-color: green
    color: #fff
</style>