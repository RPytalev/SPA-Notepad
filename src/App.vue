<template>
  <div class="container">
    <div class="header"><h1>App</h1></div>
    <div class="main">
      <div>
        <NotesListDisplay 
        :selectedNoteId="this.selectedNoteId" 
        :notesList="this.searchedNotes" 
        @note-selected="noteSelected" 
        @switch-reminder="switchReminder" 
        @delete-note="deleteNote" />
      </div>
      <div>
        <NoteEditorDisplay 
        :switchNoteEditorState="this.switchNoteEditorState" 
        :note="this.selectedNote" 
        :tagDisplayState="this.tagDisplayState"
        @create-note="createNote" 
        @edit-note="editNote" 
        @switch-component="switchComponent"
        @toggle-component="toggleComponent" 
        @change-search-tag="changeSearchTag"
        @tag-input="tagInput" />
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
        note.tags = note.rawText.match(/#[a-zA-Z0-9]+/g);
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
        // alert('Click is working ');
      },
      foundNoteSelected(id) {
        this.foundNoteId = id;
        // alert('Click is working ');
      },
      switchComponent() {
        this.switchNoteEditorState = !this.switchNoteEditorState;
      },
      toggleComponent() {
        this.switchNoteEditorState = !this.switchNoteEditorState;
      },
      changeSearchTag(searchTag) {
        this.searchTag = searchTag;
        // if (this.allTags.includes(this.inputTag, 0)) {

        //   let arr = this.notesList.filter( ( item ) => item.tags.includes(this.inputTag, 0) );
        //   this.notesListSelectedTag = this.notesListSelectedTag.concat(arr);
        //   this.switchLists = !this.switchLists;

        // } else {
        //   let stateConfirm = confirm('There is no tag. Would you like save it?');
        //   if (stateConfirm) {
        //   this.inputTag = '';
        // }
        // }
        // this.inputEvent.target.value = '';
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
    selectedFoundNote() {
      return this.notesList.filter(( item ) => item.id == this.foundNoteId)[0];
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
  
  .highlight
    font-family: Montserrat
    font-size: .8rem
    color: #ff5800
    background-color: #000

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