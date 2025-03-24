<template>
    <h2>รายชื่อวิชา</h2>
    <ul class="list-group">
      <li v-for="(subj, id) in subject" :key="id" class="list-group-item">
          <a href="#" @click="setActive(subj, $event)">
              {{ subj.id }} {{ subj.name }} (ปี{{ subj.yr }}/เทอม{{ subj.semester }})
          </a>
          <div v-if="subj.isShow">
              <SubjDetail :subjId="subj.id" @edit="showEdit(subj.id)" @delete="reload()"/>
          </div>
      </li>
    </ul>
  
    <div v-if="isEdit" class="alert alert-danger mt-3">
      มีการร้องขอแก้ไขข้อมูลของ {{ editId }}
    </div>
  </template>
  
  <script>
  import SubjDetail from './SubjDetail.vue'
  
  export default {
    name: 'SubjList',
    components: {
      SubjDetail
    },
    data() {
      return {
        subject: [],
        isEdit: false,
        editId: ''
      }
    },
    mounted() {
      this.fetchSubjects();
    },
    methods: {
      fetchSubjects() {
        fetch('http://localhost:3000/subject')
          .then(res => res.json())
          .then(data => this.subject = data)  // กำหนดค่ารายวิชา
          .catch(err => console.log(err.message))
      },
      setActive(theSubj, event) {
        event.preventDefault();
        theSubj.isShow = !theSubj.isShow;
      },
      showEdit(theSubjId) {
        this.isEdit = true;
        this.editId = theSubjId;
      },
      reload() {
        this.fetchSubjects();
      }
    }
  }
  </script>
  