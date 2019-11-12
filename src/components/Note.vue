<template>
  <div class='container layout' key='notes.length'>
    <div class='note-title'>G Note</div>
    
    <div class="floatleft" title="double click to edit note">
      <ul>
        <li @dblclick = 'getNote(index)' 
          style= "list-style-type:none;margin-top: 5px; border-radius: 5px; box-shadow: 2px 5px #888888;" 
          class="note-style" v-for='(note,index) in notes' 
          :key="note.id">
          {{note.title}} <span class='del-btn' @click='deleteNote(index)'>x</span><br>{{note.body}}
        </li><br><br>
      </ul>
    </div>

    <div class="floatright">
      <button class='row add-btn' @click='reset'>+ Add Note</button>
      <span v-if='show' style='float:left'>Title*:</span><br>
      <input v-if='show' style='float:left' v-model="title" placeholder="enter title here..."/><br><br>
      <span v-if='show' style='float:left'>Body*:</span> <br>
      <textarea v-if='show' style='float:left' v-model="body" placeholder="enter body here..."></textarea><br><br>
      <button class='add-btn btn btn-primary' v-if='!editFlag && show' :disabled="title === '' || body === '' " @click='addNote()'>Save</button>
      <button class='add-btn btn btn-primary' v-if='editFlag && show' :disabled="title === '' || body === '' " @click='editNote()'>Edit</button>
    </div>
  
  </div>
</template>

<script>
export default {
  name: 'Note',
  created: function() {
    this.notes = [
      {id:'0', title:'note 1', body: 'body 1'},
      {id:'1', title:'note 1', body: 'body 1'}
    ]
  },
  data: function() {
    return {
      title: '',
      body: '',
      notes: [],
      show: false,
      currentIndex: 0,
      editFlag: false
    }
  },
  methods: {
    addNote () {
      const newNote = {
        id: this.notes.length,
        title: this.title,
        body: this.body
      }
      this.notes.push(newNote)
      this.title = ''
      this.body = ''
    },

    getNote (index) {
      this.editFlag = true
      this.show = true
      this.currentIndex = index
      const note = this.notes[index]
      this.title = note.title
      this.body = note.body
    },
    reset () {
      this.show = true
      this.editFlag = false
      this.title = '',
      this.body = ''
    },
    editNote () {
      this.notes[this.currentIndex].title = this.title
      this.notes[this.currentIndex].body = this.body
      this.show = false
      this.title = ''
      this.body = ''
    },    
    deleteNote (index) {
      this.notes.splice(index, 1)
      this.show = false
      this.title = ''
      this.body = ''
    }
  }    
}
</script>


<style scoped>
.layout {
  border: 1px solid grey;
  height: 80%;
  background-color: #d2d2d2;
}
.note-title {
  text-align: left;
}
.note {
  border:1px slid grey;
}
li {
  hight:100px;
  width:90%;
  border:1px solid grey;
}
ul {
  margin-top: 10px;
  width:90%;
}

.add-btn {
  float: right;
}

.del-btn {
  float:right;
  margin-right:2px;
  cursor: pointer;
}

.sidenav {
  height: 75%;
  width: 160px;
  position: relative;
  z-index: 1;
  top: 20%;
  left: 5%;
  overflow-x: hidden;
  padding-top: 20px;
}

.sidenav a {
  padding: 6px 8px 6px 16px;
  text-decoration: none;
  font-size: 25px;
  color: #818181;
  display: block;
}

.sidenav a:hover {
  color: #f1f1f1;
}

.main {
  font-size: 28px; /* Increased text to enable scrolling */
  top:0px;
  float:right;
  margin-top: -170px
}


.wrap {
width: 50%;
margin: auto;
}

.floatleft {
    float:left; 
    width: 20%;
    height: 400px;
    left:0px;
    overflow-y: auto;
    border: 1px solid grey;
}

.floatright {
  float: right;   
  height: 400px;
  width: 80%;
  border: 1px solid grey;
  padding: 25px;
}

note-style {
  list-style-type:none;
  margin-top: 5px;
  width: 90%;  
}

</style>
