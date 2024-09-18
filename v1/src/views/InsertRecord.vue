<template>
  <div class="wrapper">
    <Sidebar/>
    <div class="main-panel">
      <div class="p-5 w-50">
        <h1>Instruction:</h1>
        <p>
          <span>Use the below API link to insert record</span><br/>
          <span>https://api.jlipreso.com/miit/public/api/user/insertRecord/{fname}/{lname}/{age}</span>
        </p>
        <div class="card">
          <div class="card-body">
            <table class="table">
              <tbody>
                <tr>
                  <td>First name</td>
                  <td><input class="form-control" type="text" v-model="fname" placeholder="Type first name here..."></td>
                </tr>
                <tr>
                  <td>Last name</td>
                  <td><input class="form-control" type="text" v-model="lname" placeholder="Type last name here..."></td>
                </tr>
                <tr>
                  <td>Age</td>
                  <td><input class="form-control" type="number"  v-model="age"></td>
                </tr>
                <tr>
                  <td></td>
                  <td><button class="btn btn-primary w-100" @click="insertRecord()">Submit</button></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">

  import axios from 'axios';
  import Swal from 'sweetalert2';
  import Sidebar from "@/components/Sidebar.vue";

  export default {
    name: "InsertRecord",
    components: {Sidebar},
    data() {
        return {
        fname: "",
        lname: "",
        age: 0
        }
    },

    methods: {
        async insertRecord() {
        await axios.get("https://api.jlipreso.com/miit/public/api/user/insertRecord/" + this.fname + "/" + this.lname + "/" + this.age).then( async (response) => {
            Swal.fire({
            title: "Successful",
            text: response.data?.message,
            icon: "success"
            }).then(async () => {
                this.fname = '';
                this.lname = '';
                this.age = 0;

            })
        }) ;
        }
   
  },
  }

</script>
