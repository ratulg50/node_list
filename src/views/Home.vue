<template>
  <div id="app">
      <div style="padding: 50px;">
        <button class="btn_Padding btn_create" @click="createParent()">Create Child 1</button>
      <li v-for="(category, index) in categories">
        <span> 
          {{ category.name }}
          <button class="btn_Padding btn_create" @click="createchild1(index)">Create Child 2</button>
          <button class="btn_Padding btn_delete" @click="deleteParent(index)">Delete Child 1</button>
          <button class="btn_Padding btn_edit" @click="editNameTab(index,category)">Edit Child 1</button>
          <span v-if="editTab == true && editedIndex == index">
          <input type="text" v-model="editedName">
            <button class="btn_Padding btn_delete" @click="exitNameDetails()">Exit</button>
            <button class="btn_Padding btn_create" @click="editNameDetails()">Save</button>
          </span>
        </span>
        
        <ul style="padding-left: 50px;">
          <li v-for="(job, index2) in category.jobs">
            <span>
              {{ job.name }}
              <button class="btn_Padding btn_create" @click="createchild2(index,index2)">Create Child 3</button>
              <button class="btn_Padding btn_delete" @click="deleteChild1(index,index2)">Delete Child 2</button>
              <button class="btn_Padding btn_edit" @click="editNameChild1Tab(index,index2,job)">Edit Child 2</button>
              <span v-if="editChild1Tab == true && editedIndex == index && editedChild1Index == index2">
                <input type="text" v-model="editedChild1Name">
                <button class="btn_Padding btn_delete" @click="exitNameChild1Details()">Exit</button>
                <button class="btn_Padding btn_create" @click="editNameChild1Details()">Save</button>
              </span>
            </span>
            <ul style="padding-left: 50px;">
              <li v-for="(job2, index3) in job.jobs">
                <span>
                  {{ job2.name }}
                  <button class="btn_Padding btn_delete" @click="deleteChild2(index,index2,index3)">Delete Child 3</button>
                  <button class="btn_Padding btn_edit" @click="editNameChild2Tab(index,index2,index3,job2)">Edit Child 3</button>
                  <span v-if="editChild2Tab == true && editedIndex == index && editedChild1Index == index2 && editedChild2Index == index3">
                    <input type="text" v-model="editedChild2Name">
                    <button class="btn_Padding btn_delete" @click="exitNameChild2Details()">Exit</button>
                    <button class="btn_Padding btn_create" @click="editNameChild2Details()">Save</button>
                  </span>
                </span>
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </div>
  </div>
  
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [],
      categories: [
      {
        name: "Child 1 Node",
        jobs: [
          {
            name: "Child 2 Node",
            jobs: [
              {
                name: "Child 3 Node",
                jobs: []
              },
              {
                name: "Child 3 Node",
                jobs: []
              }
            ]
          },
          {
            name: "Child 2 Node",
            jobs: [
              {
                name: "Child 3 Node",
                jobs: []
              },
              {
                name: "Child 3 Node",
                jobs: []
              }
            ]
          },
        ]
      }
    ],
    editTab: false,
    editedName:"",
    editedIndex:0,
    editedCat:[],
    editChild1Tab: false,
    editedChild1Name:"",
    editedChild1Index:0,
    editedChild1Cat:[],
    editChild2Tab: false,
    editedChild2Name:"",
    editedChild2Index:0,
    editedChild2Cat:[],
    }
  },
  methods: {
    createParent(){
      this.categories.push(
				{name: "Child 1 Node", jobs: []}
			);
      console.log("Create Child 1 Node")
      console.log(this.categories)
    },
    
    createchild1(index){
      for(let i = 0; i< this.categories.length; i++){
        if(i== index ){
          this.categories[i].jobs.push(
				    {name: "Child 2 Node", jobs: []}
			    );
        }
      }
      console.log("Create Child 2 Node")
    },
    createchild2(index, index2){
      for(let i = 0; i< this.categories.length; i++){
        if(i== index ){
          for(let j = 0; j< this.categories[i].jobs.length; j++){
            if(j== index2 ){
              this.categories[i].jobs[j].jobs.push(
                {name: "Child 3 Node", jobs: []}
              );
            }
          }
        }
      }
      console.log("Create Child 3 Node")
    },
    deleteParent(index){
      this.$delete(this.categories, index);
      console.log("delete Child 1 Node")
    },
    deleteChild1(index,index2){
      console.log(index)
      console.log(index2)
      for(let i = 0; i< this.categories.length; i++){
        if(i== index ){
          this.$delete(this.categories[i].jobs, index2);
        }
      }
      console.log("delete Child 2 Node")
    },
    deleteChild2(index,index2,index3){
      console.log(index)
      console.log(index2)
      for(let i = 0; i< this.categories.length; i++){
        if(i== index ){
          for(let j = 0; j< this.categories[i].jobs.length; j++){
            if(j== index2 ){
            this.$delete(this.categories[i].jobs[j].jobs, index3);
            }
          }
        }
      }
      console.log("delete Child 3 Node")
    },
    editNameTab(index, cat){
      this.editedIndex = index
      this.editedCat = cat
      this.editTab = true
    },
    editNameDetails(){
      this.editedCat.name = this.editedName;
      this.editedName = ""
      this.editTab = false
      console.log("Edit Child 1 Node")

    },
    exitNameDetails(){
      this.editTab = false
      this.editedName = ""
    },
    editNameChild1Tab(index,index2, cat){
      this.editedIndex = index
      this.editedChild1Index = index2
      this.editedChild1Cat = cat
      this.editChild1Tab = true
    },
    editNameChild1Details(){
      this.editedChild1Cat.name = this.editedChild1Name;
      this.editedChild1Name = ""
      this.editChild1Tab = false
      console.log("Edit Child 2 Node")

    },
    exitNameChild1Details(){
      this.editChild1Tab = false
      this.editedChild1Name = ""
    },
    editNameChild2Tab(index,index2,index3, cat){
      this.editedIndex = index
      this.editedChild1Index = index2
      this.editedChild2Index = index3
      this.editedChild2Cat = cat
      this.editChild2Tab = true
    },
    editNameChild2Details(){
      this.editedChild2Cat.name = this.editedChild2Name;
      this.editedChild2Name = ""
      this.editChild2Tab = false
      console.log("Edit Child 3 Node")

    },
    exitNameChild2Details(){
      this.editChild2Tab = false
      this.editedChild2Name = ""
    }
  },
  created() {
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }

  .btn_Padding{
        padding: 5px;
        margin: 3px;
  }
  .btn_create{
    color: white;
    background: green;
    border-radius: 5px;
  }
  
  .btn_delete{
    color: white;
    background: #ff0000b5;
    border-radius: 5px;
  }

  .btn_edit{
    color: white;
    background: orange;
    border-radius: 5px;
  }
</style>

