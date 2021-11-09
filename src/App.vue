<template>
  <div class="app-container">
    <div class="component-container">
      <div class="header">
        <div class="startTitle">Note</div>
        <div class="logo"></div>
        <div class="finishTitle">ad</div>
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
        if (this.tagDisplayState === false) {
          this.tagDisplayState = !this.tagDisplayState;
        }
        this.searchTag = '';
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
      },
      async fetchNotesList() {
        const res = await fetch('http://localhost:5000/notesList');
        const data = await res.json();
        return data
      }
    },
  data() {
    return {
      notesList: [],
      searchTag: '',
      selectedNoteId: 0,
      switchNoteEditorState: false,
      tagDisplayState: true,
    }
  },
  computed: {
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
  created() {
    this.notesList = [
        {
          "id": 1,
          "title": "",
          "rawText": "Test title 1\n test Text 1 #111",
          "tags": [
            "#111"
          ],
          "reminder": false
        },
        {
            "id": 2,
            "title": "",
            "rawText": "Test title 2\n test Text 2 #222",
            "tags": [
              "#222"
            ],
            "reminder": false
        },
        {
            "id": 3,
            "title": "",
            "rawText": "Test title 3\n test Text 3 #333",
            "tags": [
              "#333"
            ],
            "reminder": false
        }
      ],
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

*,
*::before,
*::after
  box-sizing: border-box

.app-container
  max-width: 1200px
  height: 100vh
  margin: 0px auto
  padding: 0px 15px
  background-color: #000

  .component-container
    display: flex
    flex-flow: column nowrap
    width: 100%
    height: 100%

    .highlight
      font-size: 1.4rem
      font-weight: 300
      color: #fff
      background-color: #ff7800

    .header 
      display: flex
      flex-flow: row nowrap
      width: 100%
      flex: 10%
      justify-content: center
      align-items: center
      color: #ff7800
      padding: 1rem

      .startTitle
        display: flex
        justify-self: center
        align-self: center
        width: auto
        height: 4rem
        font-size: 4rem
        font-weight: 900

      .logo
        display: flex
        justify-self: center
        align-self: center
        width: 4rem
        height: 4rem
        background-image: url(assets/logo-orange.svg)
        background-repeat: no-repeat
        background-size: contain

      .finishTitle
        display: flex
        justify-self: center
        align-self: center
        width: auto
        height: 4rem
        margin-left: -1.2rem
        font-size: 4rem
        font-weight: 900

    .main
      display: flex
      width: 100%
      flex: 80%
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
      flex: 10%

      .copyright
          color: #ff7800
          text-align: center
          padding: 1rem
</style>