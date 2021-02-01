<template>

  <div class="wrapper">
    <div class="wrapper-content">
    <section>
      <div class="container">
            <!-- <sapl/> -->
          <!-- message -->
        <message 
            v-if="message"
            :message="message"/>

        <!-- new note -->
        <newNote
            :note="note"
            @addNote="addNote"
        />


        <div class="note-header" style="margin: 36px 0">
            <!-- title -->
            <h1> {{ title }}</h1>

            <!-- search -->
            <search
                :value="search"
                placeholder="Find your Note"
                @search="search = $event"
                />

            <!-- icon control -->
            <div class="icons">
                <svg  style="cursor: pointer;"  :class="{ active: grid}" @click="grid= true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                <svg  style="cursor: pointer;"  :class="{ active: !grid }" @click="grid= false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
        </div>
        <!-- note list -->
        <notes 
            :notes="notesFilter"
            :grid="grid"
            @removeNote="removeNote"
        />

      </div>
    </section>
    </div>
  </div>
    
</template>

<script>
import message from './components/message.vue'
import newNote from './components/NewNote.vue'
import notes from './components/Notes.vue'
import Search from './components/Search.vue'

export default {
    components: {
        message, 
        newNote,
        notes,
        Search
    },
    data () {
      return {
        title: 'Notes App',
        search: '',
        message: null,
        grid: true,
        value: '',
        note: {
            title: '',
            descr: '',
            important: ''
        },
        notes: [
            {
                title: 'First Note',
                descr: 'Description for first note',
                date: new Date(Date.now()).toLocaleString(),
                important: 'Normal'
            },
            {
                title: 'Second Note',
                descr: 'Description for Second note',
                date: new Date(Date.now()).toLocaleString(),
                important: 'Important'
            },
            {
                title: 'Third Note',
                descr: 'Description for Third note',
                date: new Date(Date.now()).toLocaleString(),
                important: 'VImportant'
            }
        ]
        }
      },
      computed: {
          notesFilter () {
            let array = this.notes,
                search = this.search.trim().toLowerCase();
            if (!search) return array;
            return array = array.filter((item)=> {
                   if (item.title.toLowerCase().indexOf(search) !== -1) { return item }})
            }
      },
      methods: {
                addNote() {
                    
                    let { title, descr, important} = this.note

                    if (!title || !descr) {
                        this.message = 'Title or discription cant be blank!'
                        return false
                    }
                    this.notes.push({
                        title,
                        descr,
                        date: new Date(Date.now()).toLocaleString(),
                        important
                    })
                    this.note.title = ''
                    this.note.descr = ''
                    this.message = null
                    this.note.important = 'Normal'
                },
                removeNote(index) {
                    this.notes.splice(index,1);
                }
            }
    }

</script>

<style>

</style>

