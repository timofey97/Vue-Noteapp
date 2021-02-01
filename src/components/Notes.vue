<template>
    <div class="notes">
        
        <message 
            v-if="message"
            :message="message"/>
            <div class="note" v-for="(note, index) in notes" :class="[note.important, {full: !grid}]"  :key="index" >
                <div class="note-header" :class="{full: !grid}">
                <p contenteditable @change="change" @input="input">{{note.title}}</p>
                <p
                    style="cursor: pointer;" 
                    @click='removeNote(index)'>x
                </p>
            </div>
            <div class="note-body">
                <p>{{ note.descr}}</p>
                <span> {{ note.date }} </span>
            </div>
    </div>
    </div>
</template>

<script>
import message from './message.vue'
export default {
    components: {
        message
    },
    data() {
      return  {
          message: null
      }
    },
    props: {
        notes: {
            type: Array, 
            required: true
        },
        grid: {
            type:Boolean,
            required: true
        }
    },
    methods: {
        removeNote(index) {
            this.$emit('removeNote', index)
        },
        input(e) {
            console.log(e.target.innerText);
    },
    change(e){
        console.log(e.target.innerText);
    }
    },
    watch: { 
          notes: function(newVal) { // watch it
          newVal.length == 0 ? this.message = 'No such records were found or all records were deleted in - add new' : this.message= null
        }
}
}
</script>

<style lang="scss">
.notes {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 40px 0 ;
    }

.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #ffffff;
  transition: all .25s cubic-bezier(.02,.01,.47,1);
  box-shadow: 0 30px 30px rgba(0,0,0,.02);
  border-radius: 20px ;
  &:hover {
    box-shadow: 0 30px 30px rgba(0,0,0,.04);
    transform: translate(0,-6px);
    transition-delay: 0s !important;
  }
  &.full {
    width: 100%;
    text-align: center;
  }
}
.note-header{
    display: flex;
    align-items: center;
    justify-content: space-between;
    h1 {
        font-size: 32px;
    }
    p:first-child {
        
        text-transform: capitalize;
        color: #4400ff;
    }
    p{
        font-weight: 600;
        font-size: 22px;
        color: #ff0000;
    }
    svg {
        margin-right: 12px;
        color: #999999;
        &.active {
            color: #4400ff;
        }
        &:last-child {
            margin-right: 0;
        }
    }
    &.full {
    justify-content: center;
    p {
      margin-right: 16px;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}
.note-body {
    p {
        margin: 20px 0;
    }
    span{
        font-size: 14px;
        color: #999;
    }
}

.Normal {
    background: white;
}

.Important {
    background: #f88d0136;
}

.VImportant {
    background: #c7003833;
}
</style>

