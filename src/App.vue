<template>
  <div class="container">
    <div class="header">
      <h1>Note</h1>
      <div class="logo">
        <img id="logo" alt="Image logo Pytalev - uppercase letter P" src="assets/logo-orange.svg">
      </div>
      <h1>ad</h1>
    </div>
    <div class="main">
      <div class="notes-list-display">
        <NotesListDisplay 
        :selectedNoteId="this.selectedNoteId" 
        :notesList="this.searchedNotes" 
        @click-select-note="sendSelectedNoteId" 
        @dblclick-switch-reminder="switchReminder" 
        @btn-click-delete="deleteNote" />
      </div>
      <div class="note-editor-display">
        <NoteEditorDisplay 
        :switchNoteEditorState="this.switchNoteEditorState" 
        :note="this.selectedNote" 
        :tagDisplayState="this.tagDisplayState"
        @btn-click-create="createNote" 
        @textarea-change-edit="editNote" 
        @btn-click-toggle-display="toggleNoteDisplay"
        @mouseleave-note-editor="toggleNoteEditor"
        @btn-click-search="searchNote" />
      </div>
    </div>
    <div class="footer">
      <div class="copyright"><p>&copy; Pytalev 2021</p></div>
    </div>
  </div>
</template>

<script>
  import NotesListDisplay from './components/NoteList/Body/NotesListDisplay.vue'
  import NoteEditorDisplay from './components/NoteEditor/Body/NoteEditorDisplay.vue'

  export default {
    name: "App",
    components: {
      NotesListDisplay,
      NoteEditorDisplay
    },
    methods: {
      createNote() {
        const noteNew = {
            id: Math.floor(Math.random() * 1000),
            rawText: 'New Note\n',
            date: new Date(),
            tags: [],
            reminder: false
        }
        this.notesList.unshift(noteNew);
        this.selectedNoteId = noteNew.id;
      },
      editNote(noteChange) {
        let note = this.notesList.filter(( item ) => item.id === noteChange.id)[0];
        note.rawText = noteChange.rawText;
        note.date = noteChange.date;
        note.tags = note.rawText.match(/#[a-zA-Z0-9]+/g);
        note.tags = [...new Set(note.tags)];
        if (this.switchLists === false) {
          this.tagDisplayState = !this.tagDisplayState;
        }
        if (this.tagDisplayState === false) {
          this.tagDisplayState = !this.tagDisplayState;
        }
      },
      searchNote(searchTag) {
        this.searchTag = searchTag;
      },
      deleteNote() {
            this.notesList = this.notesList.filter(( item ) => item.id !== this.selectedNoteId);

            if (this.notesList.length === 0)
            {
              this.createNote();
            } else {
              this.selectedNoteId = this.notesList[0].id;
            }
      },
      sendSelectedNoteId(id) {
        this.selectedNoteId = id;
      },
      switchReminder(id) {
        this.notesList = this.notesList.map((item) => item.id == id ? {...item, reminder: !item.reminder} : item)
      },
      toggleNoteDisplay() {
        this.switchNoteEditorState = !this.switchNoteEditorState;
      },
      toggleNoteEditor() {
        this.switchNoteEditorState = !this.switchNoteEditorState;
      }
    },
  data() {
    return {
      notesList: [
        {
          id: 1,
          rawText: 'Test title 1\n test Text 1 #111',
          date: new Date(),
          tags: [
            '#111'
          ],
          reminder: false
        },
        {
          id: 2,
          rawText: 'Test title 2\n test Text 2 #222',
          date: new Date(),
          tags: [
            '#222'
          ],
          reminder: false
        },
        {
          id: 3,
          rawText: 'Test title 3\n test Text 3 #333',
          date: new Date(),
          tags: [
            '#333'
          ],
          reminder: false
        }
      ],
      searchTag: '',
      selectedNoteId: 0,
      switchNoteEditorState: false,
      tagDisplayState: true,
    }
  },
  computed:
  {
    selectedNote() {
      return this.notesList.filter(( item ) => item.id == this.selectedNoteId)[0];
    },
    allTags()
    {
      let allTags = new Array();
      for (let note of this.notesList)
      {
        for (let tag of note.tags)
        {
          allTags.push(tag);
        }
      }

      return allTags;
    },
    searchedNotes()
    {
      return this.searchTag === '' ? this.notesList : this.notesList.filter(note => note.tags.includes(this.searchTag, 0) )
    }
  },
  created()
  {
    this.selectedNoteId = this.notesList[0].id;
  }
}
</script>

<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;300;400;500;600;700;800;900&display=swap')

html 
  box-sizing: border-box
  margin: 0
  padding: 0
  font-size: 62.5%
  font-family: 'Montserrat', sans-serif

  h1
    font-size: 4rem
    font-weight: 900
  
  h2
    font-size: 2.4rem
    font-weight: 700
  
  h3
    font-size: 2rem
    font-weight: 400
  
  p
    font-size: 1rem
    font-weight: 300

*,
*::before,
*::after
  box-sizing: inherit

.container
  max-width: 1200px
  height: 100vh
  margin: 0px auto
  padding: 0px 15px
  background-color: #000

  .highlight
    font-size: 1.4rem
    font-weight: 300
    color: #fff
    background-color: #ff7800

  .header 
    display: flex
    width: 100%
    height: 10vh
    justify-content: center
    color: #ff7800
    text-align: center
    padding: 1rem

    .logo
      display: flex
      justify-content: center
      align-items: center
      width: 4rem
      height: 4rem

      img
        width: 4rem
        height: 4rem
        object-fit: contain
  
  .main
    display: flex
    width: 100%
    height: 80vh
    background-color: #e9e9e9

    .notes-list-display
      display: flex
      flex-flow: column
      align-items: flex-start
      flex-basis: 30%
      background-color: rgb(42, 39, 39)
      color: lightgrey
      border-right: .1rem solid #000
      overflow-y: scroll
    
    .note-editor-display
      display: flex
      flex-flow: column
      flex-basis: 70%

  .footer
    display: flex
    justify-content: center
    align-items: center
    width: 100%
    height: 10vh

    .copyright
        color: #ff7800
        text-align: center
        padding: 1rem
</style>