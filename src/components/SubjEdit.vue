<template>
    <div class="card mt-3 p-3">
      <h5>แก้ไข</h5>
      <form @submit.prevent="handleUpdate()">

        <label>รหัสวิชา</label>
        <input type="text" v-model="subject.id" class="form-control" />

        <label>ชื่อวิชา</label>
        <input type="text" v-model="subject.name" class="form-control" />
  
        <label>หน่วยกิต</label>
        <select v-model="subject.credit" class="form-select">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
          <option value="4">4</option>
        </select>
  
        <label>เกรด</label>
        <select v-model="subject.grade" class="form-select">
          <option value="A">A</option>
          <option value="B+">B+</option>
          <option value="B">B</option>
          <option value="C+">C+</option>
          <option value="C">C</option>
          <option value="D+">D+</option>
          <option value="D">D</option>
          <option value="F">F</option>
        </select>

        <label>ปี</label>
        <select v-model="subject.yr" class="form-select">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
          <option value="4">4</option>
        </select>

        <label>เทอม</label>
        <select v-model="subject.semester" class="form-select">
          <option value="1">1</option>
          <option value="2">2</option>
        </select>
  
        <button type="submit" class="btn btn-success mt-2">บันทึกการแก้ไข</button>
        <button type="button" class="btn btn-secondary mt-2 ms-2" @click="$emit('cancel')">ยกเลิก</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SubjEdit',
    props: ['subjId'],
    data() {
      return {
        subject: {},
      };
    },
    mounted() {
      fetch('http://localhost:3000/subject/' + this.subjId)
        .then(res => res.json())
        .then(data => this.subject = data)
        .catch(err => console.log(err.message));
    },
    methods: {
      handleUpdate() {
        fetch('http://localhost:3000/subject/' + this.subjId, {
          method: 'PUT',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(this.subject),
        })
        .then(() => this.$emit('updated'))
        .catch(err => console.log(err.message));
      }
    }
  };
  </script>
  