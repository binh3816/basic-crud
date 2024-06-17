<template>
  <div>
    <button @click="showModal">Add Student</button>
    <button @click="showSearch">Search</button>
    <Teleport to="#portal-root">
      <ModalComponent :isVisible="isVisible" @close="isVisible = false">
        <form @submit.prevent="addStudent">
          <label for="name">Name</label>
          <input type="text" id="name" name="name" v-model="formData.name" />
          <br />
          <label for="age">Age</label>
          <input type="number" id="age" name="age" v-model="formData.age" />
          <br />
          <label for="major">Major</label>
          <input type="text" id="major" name="major" v-model="formData.major" />
          <br />
          <label for="gpa">GPA</label>
          <input type="number" id="gpa" name="gpa" v-model="formData.gpa" />
          <br />
          <label for="email">Email</label>
          <input
            type="email"
            id="email"
            name="email"
            v-model="formData.email"
          />
          <br />
          <label for="enrolled">Enrolled</label>
          <input
            type="checkbox"
            id="enrolled"
            name="enrolled"
            v-model="formData.enrolled"
          />
          <br />
          <button type="submit">Add</button>
        </form>
      </ModalComponent>
    </Teleport>
    <Teleport to="#portal-root">
      <ModalComponent
        :isVisible="isSearchVisible"
        @close="isSearchVisible = false"
      >
        <form @submit.prevent="searchStudents">
          <label for="name">Name</label>
          <input type="text" id="name" name="name" v-model="searchData.name" />
          <br />
          <label for="major">Major</label>
          <select id="major" name="major" v-model="searchData.major">
            <option value="Computer Science">Computer Science</option>
            <option value="Mathematics">Mathematics</option>
            <option value="Physics">Physics</option>
            <option value="Chemistry">Chemistry</option>
            <option value="Biology">Biology</option>
          </select>
          <br />
          <label for="enrolled">Enrolled</label>
          <input
            type="checkbox"
            id="enrolled"
            name="enrolled"
            v-model="searchData.enrolled"
          />
          <br />
          <button type="submit">Search</button>
        </form>
      </ModalComponent>
    </Teleport>
    <DataList ref="dataList"></DataList>
  </div>
</template>

<script>
import DataList from "./components/DataList.vue";
import ModalComponent from "./components/ModalComponent.vue";
export default {
  name: "App",
  components: {
    DataList,
    ModalComponent,
  },
  data() {
    return {
      isVisible: false,
      isSearchVisible: false,
      formData: {
        name: "",
        age: "",
        major: "",
        gpa: "",
        email: "",
        enrolled: false,
      },
      searchData: {
        name: "",
        major: "",
        enrolled: false,
      },
    };
  },
  methods: {
    showModal() {
      this.isVisible = true;
    },
    showSearch() {
      this.isSearchVisible = true;
    },
    addStudent() {
      this.$refs.dataList.addStudent(this.formData);
      this.isVisible = false;
    },
    searchStudents() {
      this.$refs.dataList.searchStudents(this.searchData);
      this.isSearchVisible = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

form input:not([type="checkbox"]),
form textarea {
  display: block;
  width: 400px;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  color: #555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-bottom: 15px;
}

form button {
  display: block;
  width: 100px;
  padding: 6px 12px;
  font-size: 14px;
  font-weight: bold;
  line-height: 1.42857143;
  color: #fff;
  background-color: #42b983;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin: 0 auto;
}
</style>
