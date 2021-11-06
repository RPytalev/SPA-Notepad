<template>
  <div class="container">
    <div class="header"><h1>App</h1></div>
    <div class="main">
      <div>
        <NotesListDisplay 
        :selectedNoteId="selectedNoteId" 
        :notesList="notesList" 
        :notesListSelectedTag="notesListSelectedTag"
        :switchLists="switchLists"
        @note-selected="noteSelected" 
        @switch-reminder="switchReminder" 
        @delete-note="deleteNote" />
      </div>
      <div>
        <NoteEditorDisplay 
        :switchNoteEditorState="switchNoteEditorState" 
        :note="selectedNote" 
        :tagDisplayState="tagDisplayState"
        @create-note="createNote" 
        @edit-note="editNote" 
        @switch-component="switchComponent" 
        @toggle-component="toggleComponent" 
        @search-tag="searchTag"
        @tag-input="tagInput"
        @delete-tag="deleteTag" />
      </div>
    </div>
    <div class="footer"></div>
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
        let arr = note.rawText.match(/#[a-z A-Z 0-9]+/g);
        this.tagsList.push(...arr);
        this.tagsList = [...new Set(this.tagsList)];
        note.tags.push(...arr);
        note.tags = [...new Set(note.tags)];
        if (this.switchLists === false) {
          this.switchLists = !this.switchLists;
          this.tagDisplayState = !this.tagDisplayState;
        }
        if (this.tagDisplayState === false) {
          this.tagDisplayState = !this.tagDisplayState;
        }
      },
      switchReminder(id) {
        this.notesList = this.notesList.map((item) => item.id == id ? {...item, reminder: !item.reminder} : item)
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
      noteSelected(id) {
        this.selectedNoteId = id;
      },
      switchComponent() {
        this.switchNoteEditorState = !this.switchNoteEditorState;
      },
      toggleComponent() {
        this.switchNoteEditorState = !this.switchNoteEditorState;
      },
      searchTag() {

        if (this.tagsList.includes(this.inputTag, 0)) {

          let arr = this.notesList.filter( ( item ) => String(item.tags) === this.inputTag );
          console.log(arr);
          this.notesListSelectedTag = this.notesListSelectedTag.concat(arr);
          console.log(this.notesListSelectedTag);
          this.switchLists = !this.switchLists;

        } else {
          let stateConfirm = confirm('There is no tag. Would you like save it?');
          if (stateConfirm) {
          this.tagsList.push(this.inputTag);
          this.inputTag = '';
        }
        }
        this.inputEvent.target.value = '';
      },
      tagInput(inputTag, event) {
        this.inputTag = inputTag;
        this.inputEvent = event;
      },
      deleteTag(tag) {
        let stateConfirm = confirm('Are you sure?');
        if (stateConfirm) {
          this.tagsList = this.tagsList.filter((item) => String(item) !== tag);
          this.tagDisplayState = !this.tagDisplayState;
        }
      }
    },
  data() {
    return {
      notesList: [
        {
          id: 1,
          rawText: 'Test title 1\n test Text 1',
          date: new Date(),
          tags: [],
          reminder: false
        },
        {
          id: 2,
          rawText: 'Test title 2\n test Text 2',
          date: new Date(),
          tags: [],
          reminder: false
        },
        {
          id: 3,
          rawText: 'Test title 3\n test Text 3',
          date: new Date(),
          tags: [],
          reminder: false
        }
      ],
      tagsList: [],
      selectedNoteId: 0,
      switchNoteEditorState: false,
      inputTag: '',
      inputEvent: {},
      notesListSelectedTag: [],
      switchLists: true,
      tagDisplayState: true
    }
  },
  computed:
  {
    selectedNote: function() {
      return this.notesList.filter(( item ) => item.id == this.selectedNoteId)[0];
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
$primary-color: #ff5800
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