<template>
    <div class="card">
      <div class="card-body">
        <form @submit.prevent="handleSubmit()">
          <div class="row">
              <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
                  <label for="subjId" class="form-label">รหัสวิชา</label>
                  <input type="text" id="subjId" class="form-control" v-model.trim="subjs.id" />
              </div>
              <div class="col-lg-4 col-md-8 col-sm-6 mt-2">
                  <label for="subjName" class="form-label">ชื่อวิชา</label>
                  <input type="text" id="subjName" class="form-control" v-model.trim="subjs.name" />
              </div>
              <div class="col-lg-2 col-md-8 col-sm-6 mt-2">
                  <label for="subjCredit" class="form-label">หน่วยกิต</label>
                  <select id="subjCredit" class="form-select" v-model="subjs.credit">
                      <option value="1">1</option>
                      <option value="2">2</option>
                      <option value="3">3</option>
                      <option value="4">4</option>
                  </select>
              </div>
              <div class="col-lg-2 col-md-8 col-sm-6 mt-2">
                  <label for="subjGrade" class="form-label">เกรด</label>
                  <select id="subjGrade" class="form-select" v-model="subjs.grade">
                      <option value="A">A</option>
                      <option value="B+">B+</option>
                      <option value="B">B</option>
                      <option value="C+">C+</option>
                      <option value="C">C</option>
                      <option value="D+">D+</option>
                      <option value="D">D</option>
                      <option value="F">F</option>
                  </select>
              </div>
              <div class="col-lg-2 col-md-8 col-sm-6 mt-2">
                  <label for="subjYr" class="form-label">ชั้นปี</label>
                  <select id="subjYr" class="form-select" v-model="subjs.yr">
                      <option value="1">1</option>
                      <option value="2">2</option>
                      <option value="3">3</option>
                      <option value="4">4</option>
                  </select>
              </div>
              <div class="col-lg-2 col-md-8 col-sm-6 mt-2">
                  <label for="subjSemester" class="form-label">ภาคเรียน</label>
                  <select id="subjSemester" class="form-select" v-model="subjs.semester">
                      <option value="1">1</option>
                      <option value="2">2</option>
                  </select>
              </div>
              <div class="col-12 d-flex justify-content-center mt-2">
                <button id="btnSubmit" type="submit" class="btn btn-primary">บันทึก</button>
              </div>
          </div>
        </form>
      </div>
    </div>
    <div class="alert alert-success mt-2" v-show="addSuccess">
      บันทึกข้อมูล {{ subjs.id }} - {{ subjs.name }} สำเร็จ
    </div>
    <div class="alert alert-danger mt-2" v-show="addError">
      {{ errMessage }}
    </div>
  </template>
  
  <script>
  export default {
      name: 'SubjAdd',
      data() {
          return {
              subjs: {
                  id: "",
                  name: "",
                  credit: "",
                  grade: "",
                  yr: 2,
                  semester: 2,
                  isShow: false,
              },
              addSuccess: false,
              addError: false,
              errMessage: ""
          }
      },
      methods: {
        // Method ที่ทำงานเมื่อมีการ Submit
        handleSubmit() {
            // สร้าง Object เพื่อเตรียมส่งข้อมูล - ค่า properties ที่ v-model กับ form ไว้
            let subject = {
                id: this.subjs.id,
                name: this.subjs.name,
                credit: this.subjs.credit,
                grade: this.subjs.grade,
                yr: this.subjs.yr,
                semester: this.subjs.semester,
                isShow: false
            }
            // กำหนดการติดต่อกับ endpoint ระบุ Method POST
            fetch('http://localhost:3000/subject', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(subject)
            })
            .then(() => {
                this.addSuccess = true
                this.addError = false
                this.resetForm()  // รีเซ็ตฟอร์มหลังจากบันทึกข้อมูล
            })
            .catch((err) => {
                this.addError = true
                this.errMessage = err.message
            })
        },
        // รีเซ็ตฟอร์มเมื่อบันทึกสำเร็จ
        resetForm() {
            this.subjs = {
                id: "",
                name: "",
                credit: "",
                grade: "",
                yr: 2,
                semester: 2,
                isShow: false
            }
        }
      }
  }
  </script>
  
  <style>
  /* เพิ่มสไตล์ถ้าต้องการ */
  </style>
  