<template>
  <!-- Get All Data -->
  <div>
    <div>
      <h2>Get All Data</h2>
      <div>
        <button @click="getAllData">Get All Data</button>
      </div>
      <br />
      <div>
        <table border="1px">
          <tr>
            <td>Id</td>
            <td>Title</td>
            <td>Body</td>

            <td>Action</td>
          </tr>
          <tr v-for="item in getData" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.title }}</td>
            <td>{{ item.body }}</td>
            <td><button @click="deleteData(item.id)">Delete</button></td>
          </tr>
          <h3 v-if="errorMsg">{{ errorMsg }}</h3>
        </table>
      </div>
    </div>
    <!-- Create Post -->
    <div>
      <div><h2>Create Post</h2></div>
      <div>
        <form @submit.prevent="createPost">
          <div>
            <input
              type="text"
              id="User_ID"
              placeholder="User ID"
              v-model="formData.userId"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Post_Title"
              placeholder="Post Title"
              v-model="formData.title"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Post_Body"
              placeholder="Post Body"
              v-model="formData.body"
            />
          </div>
          <br />
          <button>Create Post</button>
        </form>
      </div>
    </div>
    <!-- Update Post -->
    <div>
      <div><h2>Update Post</h2></div>
      <div>
        <form @submit.prevent="updatePost">
          <div>
            <input
              type="text"
              id="Update_Id"
              placeholder="Update Id"
              v-model="formData.id"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Update_User_ID"
              placeholder="Update User ID"
              v-model="formData.userId"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Update_Title"
              placeholder="Update Title"
              v-model="formData.title"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Update_Body"
              placeholder="Update Body"
              v-model="formData.body"
            />
          </div>
          <br />
          <button>Update Data</button>
        </form>
      </div>
    </div>
    <!-- Patching Post -->
    <div>
      <div><h2>Patching Post</h2></div>
      <div>
        <form @submit.prevent="patchData">
          <div>
            <input
              type="text"
              id="Patch_Id"
              placeholder="Patch Id"
              v-model="formData.id"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Patch_User_ID"
              placeholder="Patch User ID"
              v-model="formData.userId"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Patch_Title"
              placeholder="Patch Title"
              v-model="formData.title"
            />
          </div>
          <br />
          <div>
            <input
              type="text"
              id="Patch_Body"
              placeholder="Patch Body"
              v-model="formData.body"
            />
          </div>
          <br />
          <button>Patch Data</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "JpmKiTee",
  data() {
    return {
      getData: [],
      errorMsg: "",
      formData: {
        id: "",
        title: "",
        body: "",
        userId: "",
      },
    };
  },
  methods: {
    getAllData() {
      axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then((responce) => {
          console.log(responce.data);
          this.getData = responce.data;
        })
        .catch((error) => {
          console.log(error);
          this.errorMsg = "Error retrieving data";
        });
    },
    createPost() {
      axios
        .post("https://jsonplaceholder.typicode.com/posts", this.formData)

        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
          this.errorMsg = "Error retrieving data";
        });
    },
    updatePost() {
      axios
        .put("https://jsonplaceholder.typicode.com/posts/1", this.formData)
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
          this.errorMsg = "Error retrieving data";
        });
    },
    patchData() {
      axios
        .patch("https://jsonplaceholder.typicode.com/posts/1", this.formData)
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
          this.errorMsg = "Error retrieving data";
        });
    },
    deleteData(id) {
      axios
        .delete("https://jsonplaceholder.typicode.com/posts/1" + id)
        .then(() => this.getAllData());
    },
  },
};
</script>

<style scoped>
table,
input,
button {
  border-collapse: collapse;
}

td,
th,
input,
button {
  border: 1px solid #999;
  padding: 0.5rem;
  text-align: left;
}
</style>