<template>
  <div id="app">
  <NewSudentForm v-on:student-added="newStudentAdded"></NewSudentForm>

  <studentTable v-bind:students="students"
  v-on:student-present="studentArrivedOrLeft"
  v-on:delete-student="studentDeleted">
  </StudentTable>

  <studentMessage v-bind:message="message" v-bind:name="name"></studentMessage>
  </div>
</template>

<script>
import NewSudentForm from './components/NewSudentForm.vue'
import studentMessage from './components/studentMessage.vue'
import studentTable from './components/studentTable.vue'

export default {
  name: 'App',
  components: {
    NewSudentForm,
    studentMessage,
    studentTable
  },
  data() {
    return{
      students: [],
      message:'',
      name:''
      
    }
  },
  methods: {
    newStudentAdded(student) {
      this.students.push(student)
      this.students.sort(function (s1, s2){
        return s1.name.toLowerCase() < s2.name.toLowerCase() ? -1: 1
      })
    }, 
    studentArrivedOrLeft(student) {
      this.message = student.present ? 'welcome, ' : 'Goodbye, '
      this.name= student.name
    
  },
  studentDeleted(student) {
    this.students = this.students.filter( s => s != student )
  }
    

  }
}
</script>

<style>

</style>
