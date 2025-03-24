<template>
  <div class="container">
    <h1 class="pt-5 text-primary">Portfolio</h1>
    <h3 class="pt-5 text-primary opacity-75">Nontawat Phunpuek</h3>
    <br>
    <img src="pic.jpg" alt="Nontawat" class="profile-image">
    <br><br>
    <div class="info">
      <h4 class="text"> ประวัติ </h4>
      <p class="text">ชื่อ: {{ name }}</p>
      <p class="text">รหัสนิสิต: {{ id }}</p>
      <p class="text">คณะ: {{ faculty }}</p>
      <p class="text">สาขา: {{ major }}</p>
      <p class="text">งานอดิเรก: {{ hobby }}</p>
    </div>

    <div class="btn-group">
      <button class="btn btn-primary mx-1" @click="toggleList()">แสดงวิชาที่เรียน</button>
      <button class="btn btn-primary mx-1" @click="toggleAdd()">เพิ่มวิชา</button>
    </div>

    <div class="m-2" v-if="showSubjList">
      <SubjList />
    </div>

    <div class="m-2" v-if="showSubjAdd">
      <SubjAdd />
    </div>
  </div>
</template>

<script>
  import SubjAdd from './components/SubjAdd.vue'
  import SubjList from './components/SubjList.vue'

  export default {
    name: 'App',
    components: {
      SubjList,
      SubjAdd
    },
    data() {
      return {
        name: "นายนนทวัฒน์ พันธ์เผือก",
        id: "6530200673",
        faculty: "วิทยาศาสตร์ ศรีราชา",
        major: "วิทยาการคอมพิวเตอร์ (S05)",
        hobby: "ฟังเพลง, เล่นเกม, เตะบอล, อ่านการ์ตูน",
        showSubjList: false,
        showSubjAdd: false
      }
    },
    methods: {
      toggleList() {
        this.showSubjList = !this.showSubjList
        this.showSubjAdd = false
      },
      toggleAdd() {
        this.showSubjAdd = !this.showSubjAdd
        this.showSubjList = false
      }
    }
  }
</script>

<style scoped>
  .container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    text-align: center;
  }

  .profile-image {
    border-radius: 50%;
    width: 200px;
    height: 200px;
    object-fit: cover;
    border: 3px solid #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  .info {
    margin-top: 20px;
    margin-bottom: 30px;
  }

  .text {
    margin: 5px 0;
  }

  .btn-group {
    margin-bottom: 20px;
  }

  .btn {
    border-radius: 20px;
  }
</style>
