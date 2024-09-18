<template>
  <div class="wrapper">
    <Sidebar/>
    <div class="main-panel">
      <div class="p-5 w-75">
        <h1>Instruction:</h1>
        <p>
          <span>Get Records using the below API link:</span><br/>
          <span>https://api.jlipreso.com/miit/public/api/user/getAll</span>
        </p>
        <div class="card">
          <div class="card-body">
            <button class="btn btn-primary" @click="getRecord()">Get All Users</button>
            <table class="table table-striped mt-5">
              <thead>
                <tr>
                  <th class="bg-dark text-white">Number</th>
                  <th class="bg-dark text-white">First name</th>
                  <th class="bg-dark text-white">Last name</th>
                  <th class="bg-dark text-white">Age</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(user, i) in 3" :key="i">
                  <td>{{ (i + 1) }}</td>
                  <td></td>
                  <td></td>
                  <td></td>

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
  import Swal from 'sweetalert2'
  import Sidebar from "@/components/Sidebar.vue";


  export default {
    name: "getRecord",
    components: {Sidebar},
    data() {
      return {
        users: {} as any,
        id: 0
      }
    },
    methods: {
      async getRecord() {
        await axios.get("https://api.jlipreso.com/miit/public/api/user/getAll").then(async (response) => {
          this.users = response.data;
        });
      },
      async editAge(user: any) {
        Swal.fire({
          title: "Enter new age",
          input: "text",
          inputAttributes: {
            autocapitalize: "off"
          },
          showCancelButton: true,
        }).then(async (result) => {
          if (result.isConfirmed) {
            await axios.get("http://127.0.0.1:8000/api/user/updateRecord/" + user?.dataid + "/" + result.value).then(async () => {
              this.getRecord();
            });
            }
        });
       
      },
      async deleteRecords(user: any) {
        Swal.fire({
          title: "Confirmation",
          text: "Delete selected user?",
          icon: "warning",
          showCancelButton: true,
          confirmButtonText: "Yes, delete it!",
        }).then(async (result) => {
          if (result.isConfirmed) {
            await axios.get("http://127.0.0.1:8000/api/user/deleteByID/" + user?.dataid).then( async () => {
              this.getRecord();
            });
           }
        });
      }
    }
  
  }
  </script>
  <style scope>
  .container-bar {
    border: 3px solid black;
  }
  </style>
