<template>
  <div class="container">
    <div class="header"><h1>App</h1></div>
    <div class="main">
      <div>
        <NotesListDisplay :selectedNoteId="selectedNoteId" :notesList="notesList" @note-selected="noteSelected" @switch-reminder="switchReminder" @delete-note="deleteNote" />
      </div>
      <div>
        <Note :note="selectedNote" @edit-note="editNote" @create-note="createNote" />
      </div>
    </div>
    <div class="footer"></div>
  </div>
</template>

<script>
  import NotesListDisplay from './components/NoteList/Body/NotesListDisplay.vue'
  import Note from './components/NoteEditor/Body/Note.vue'

  export default {
    name: "App",
    components: {
      NotesListDisplay,
      Note
    },
    methods: {
      createNote() {
        const noteNew = {
            id: Math.floor(Math.random() * 1000),
            rawText: 'New Note\n',
            date: new Date(),
            reminder: false
        }

        this.notesList = [...this.notesList, noteNew];
        this.selectedNoteId = noteNew.id;
        //this.notesList = this.notesList.filter(( item ) => item.id !== this.selectedNoteId);

        // for (var i = 0; i < tagsNew.length; i++) {

	      //   if(this.tagsList.includes(tagsNew[i], 0)) {
	      //   	return;
	      //   } 	
	      //     this.tagsList.push(tagsNew[i]);
        //     this.selectedNote = 0;
        // } 
      },
      editNote(noteChange) {
        let note = this.notesList.filter(( item ) => item.id === noteChange.id)[0];
        note.rawText = noteChange.rawText;
        note.date = noteChange.date;
      },
      switchReminder(id) {
        this.notesList = this.notesList.map((item) => item.id == id ? {...item, reminder: !item.reminder} : item)
      },
      deleteNote() {
            this.notesList = this.notesList.filter(( item ) => item.id !== this.selectedNoteId);
            this.selectedNoteId = 1;
      },
      noteSelected(id) {
        this.selectedNoteId = id;
      },
      // findTag() {
      //   let arr = this.notesList.map(( item )=> item = item.text);
      //   let str = String(arr);
      //   let arrTags = str.match(/#[a-z A-Z 0-9]+/g);
      //   this.tagsList = this.tagsList.concat(arrTags);
      //   return this.tagsList;
      // }
    },
  data() {
    return {
      notesList: [
        {
          id: 1,
          rawText: 'Test title 1\n test Text 1',
          date: 'November 1st 22:00 pm',
          tags: [],
          reminder: false
        },
        {
          id: 2,
          rawText: 'Test title 2\n test Text 2',
          date: 'December 2nd 15:00 pm',
          tags: [],
          reminder: false
        },
        {
          id: 3,
          rawText: 'Test title 3\n test Text 3',
          date: 'December 3rd 7:00 am',
          tags: [],
          reminder: false
        }
      ],
      selectedNoteId: 1,
      showNewTextarea: false
    }
  },
  computed:
  {
    selectedNote: function() {
      return this.notesList.filter(( item ) => item.id == this.selectedNoteId)[0];
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