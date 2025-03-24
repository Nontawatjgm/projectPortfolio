<template>
    <div class="card my-2">
        <div class="card-body bg-success bg-opacity-25">
            <h5 class="card-title">รหัสวิชา {{ subject.id }}</h5>
            <div class="card-sub-title">วิชา {{ subject.name }}</div>
            <div class="card-sub-title">ปี {{ subject.yr }} เทอม{{ subject.semester}}</div>
            <div class="cart-text">หน่วยกิต {{ subject.credit }} เกรด {{ subject.grade }}</div>
        </div>
    </div>
    <button class="btn btn-danger" @click="delDetail(subjId)">ลบข้อมูล</button>
    <div v-if="isDeleted" class="alert alert-success mt-2" role="alert">
        ข้อมูลถูกลบเรียบร้อยแล้ว!
    </div>
    <div v-if="deleteError" class="alert alert-danger mt-2" role="alert">
        เกิดข้อผิดพลาดในการลบข้อมูล!
    </div>
</template>

<script>
export default {
    name: 'SubjDetail',
    props: ['subjId'],
    data() {
        return {
            subject: [],
            isDeleted: false,
            deleteError: false
        }
    },
    mounted() {
        fetch('http://localhost:3000/subject/' + this.subjId)
            .then(res => res.json())
            .then(data => this.subject = data)
            .catch(err => console.log(err.message))
    },
    methods: {
        editDetail(theId) {
            this.$emit('edit', theId)
        },
        delDetail(theId) {
            fetch('http://localhost:3000/subject/' + theId, {
                method: 'DELETE'
            })
            .then(response => {
                if (response.ok) {
                    this.isDeleted = true
                    this.deleteError = false
                    this.$emit('delete') // ส่งสัญญาณลบสำเร็จ
                } else {
                    throw new Error('ลบไม่สำเร็จ')
                }
            })
            .catch(() => {
                this.deleteError = true
                this.isDeleted = false
            })
        }
    }
}
</script>

<style scoped>
/* เพิ่มสไตล์เพื่อให้ข้อความแจ้งเตือนดูดี */
.alert {
    text-align: center;
}
</style>
