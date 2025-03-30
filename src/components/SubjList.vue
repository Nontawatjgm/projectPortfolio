<template>
  <h2>รายชื่อวิชา</h2>
  <ul class="list-group">
    <li v-for="(subj, id) in subject" :key="id" class="list-group-item">
      <a href="#" @click="setActive(subj, $event)">
        {{ subj.id }} {{ subj.name }} (ปี{{ subj.yr }}/เทอม{{ subj.semester }})
      </a>

      <div v-if="subj.isShow">
        <SubjDetail :subjId="subj.id" @edit="showEdit(subj.id)" @delete="reload()" />
      </div>
    </li>
  </ul>

  <!-- แสดงฟอร์มแก้ไขข้อมูล -->
  <SubjEdit v-if="isEdit" :subjId="editId" @updated="reloadEdit()" @cancel="cancelEdit()" />
</template>

<script>
import SubjDetail from './SubjDetail.vue';
import SubjEdit from './SubjEdit.vue';

export default {
  name: 'SubjList',
  components: {
    SubjDetail,
    SubjEdit
  },
  data() {
    return {
      subject: [],
      isEdit: false,
      editId: ''
    };
  },
  mounted() {
    this.fetchSubjects();
  },
  methods: {
    fetchSubjects() {
      fetch('http://localhost:3000/subject')
        .then(res => res.json())
        .then(data => this.subject = data)
        .catch(err => console.log(err.message));
    },
    setActive(theSubj, event) {
      event.preventDefault();
      theSubj.isShow = !theSubj.isShow;
    },
    showEdit(theSubjId) {
      this.isEdit = true;
      this.editId = theSubjId;
    },
    reloadEdit() {
      this.isEdit = false;
      this.fetchSubjects();
    },
    cancelEdit() {
      this.isEdit = false;
    },
    reload() {
      this.fetchSubjects();
    }
  }
};
</script>
