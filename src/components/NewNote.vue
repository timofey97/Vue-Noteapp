<template >
     <div class="new-note">
            <div class="titleBlock">
                <div class="titleContent">
                    <label>Title</label>
                    <input v-model="note.title" type="text">
                </div>

                <div class='impRadio'>
                    <input type="radio" id="one" value="Normal" v-model="note.important">
                    <label for="one">Normal</label>
                    <br>
                    <input type="radio" id="two" value="Important" v-model="note.important">
                    <label style="color: #f88f01" for="two">Important</label>
                    <br>
                    <input type="radio" id="three" value="VImportant" v-model="note.important">
                    <label style="color: #c70039"for="three">Very important</label>
                </div>
            </div>
            <label class="descr">Description</label>
            <textarea v-model="note.descr"></textarea> <br/>
            <button class="btn btnPrimary btndd" @click="addNote">New note</button>    
        </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object, 
            required: true,
        }
    },
    methods: {
        addNote() {
            this.$emit('addNote', this.note)
        },
        
    }
}
</script>

<style lang="scss" solid>
.new-note {

}

.descr {
    margin: 15px;
}
textarea {
    margin: 0 20% 0 20% ; 
}
.btndd {
    position: relative;
left: 45%;
    transition: all .25s cubic-bezier(.02,.01,.47,1);
  box-shadow: 0 30px 30px rgba(0,0,0,.02);
  border-radius: 20px ;
  &:hover {
    box-shadow: 0 30px 30px rgba(0,0,0,.04);
    transform: translate(0,-6px);
    transition-delay: 0s !important;
}
}

.titleBlock {
    display: flex;
    justify-content: space-between;
    height: 150px;
    align-items: center;
}

.titleContent {
    margin: 0;
    flex-grow: 1;
    label {
        margin: 15px;
    }
    input {
        margin: 0;
        width: 100%;
    }
}
.impRadio {
    border: 1px solid #DCDFE6;
        padding: 16px 26px;
            border-radius: 20px;
            background: white;
    margin: 20px;
    width: 20%;
    align-items: center;
    input {
        width: 10% !important;
        margin-bottom: 10px !important;
    }
}



</style>