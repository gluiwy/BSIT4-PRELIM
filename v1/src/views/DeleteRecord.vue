<template>
  <div class="wrapper">
    <Sidebar/>
    <div class="main-panel">
      <div class="p-5">
        <h1>Instruction:</h1>
        <p>
          <span>Delete Record using the below link:</span><br/>
          <span>https://api.jlipreso.com/miit/public/api/user/deleteByID/{id}</span>
        </p>
        
          <div class="card-body">
            <table class="table">
              <tbody>
                <tr>
                  <td style="width: 50px;">ID</td>
                  <td><input class="form-control" type="number" v-model="id" placeholder="Enter ID to delete"></td>
                  <td><button class="btn btn-danger" @click="deleteRecord">Delete</button></td>
                </tr>
              </tbody>
            </table>
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
    components: { Sidebar },
    data() {
      return {
        id: 0,
      }
    },
    methods: {
      async deleteRecord() {
        if (this.id > 0) {
          try {
            const response = await axios.get(`https://api.jlipreso.com/miit/public/api/user/deleteByID/${this.id}`);
            
            
            Swal.fire({
              title: "Deleted!",
              text: response.data?.message || "Record deleted successfully!",
              icon: "success"
            }).then(() => {
              this.id = 0;
            });

          } catch (error) {
            // Handle error if the deletion fails
            Swal.fire({
              title: "Error",
              text: error.response?.data?.message || "Failed!",
              icon: "error"
            });
          }
        } else {
          // If no valid ID is entered, show a warning
          Swal.fire({
            title: "Error",
            text: "Enter a valid ID.",
            icon: "warning"
          });
        }
      }
    }
  }
</script>

<style scoped>
.container-bar {
  border: 3px solid black;
}
</style>
