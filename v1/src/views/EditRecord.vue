<template>
  <div class="wrapper">
    <Sidebar/>
    <div class="main-panel">
      <div class="p-5 w-75">
        <h1>Instruction:</h1>
        <p>
          <span>Update Age using the below link:</span><br/>
          <span>https://api.jlipreso.com/miit/public/api/user/updateRecord/{id}/{age}</span>
        </p>

        <div class="card">
          <div class="card-body">
            <table class="table">
              <tbody>
                <tr>
                  <td style="width: 50px;">ID</td>
                  <td><input class="form-control" v-model="id" type="text" placeholder="Enter ID"></td>
                  <td style="width: 50px;">Age</td>
                  <td><input class="form-control" v-model="newAge" type="number" placeholder="Enter New Age"></td>
                  <td><button class="btn btn-primary" @click="editAge()">Update Age</button></td>
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
    name: "EditRecord",
    components: { Sidebar },
    data() {
      return {
        id: "",
        newAge: 0 
      };
    },
    methods: {
      async editAge() {
        if (this.id && this.newAge > 0) {
          try {
            const response = await axios.get(`https://api.jlipreso.com/miit/public/api/user/updateRecord/${this.id}/${this.newAge}`);
            
            Swal.fire({
              title: "Successful",
              text: response.data?.message || "Record Updated Successfully!",
              icon: "success"
            }).then(() => {
              this.id = 0;
              this.newAge = 0;
            });

          } catch (error) {
            Swal.fire({
              title: "Error",
              text: error.response?.data?.message || "An error occurred",
              icon: "error"
            });
          }
        } else {
          Swal.fire({
            title: "Error",
            text: "Please provide a valid ID and age.",
            icon: "warning"
          });
        }
      }
    }
  }
</script>
