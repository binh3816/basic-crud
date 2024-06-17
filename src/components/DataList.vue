<template>
  <div>
    <h1>Student Information</h1>
    <table>
        <thead>
          <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Age</th>
            <th>Major</th>
            <th>Gpa</th>
            <th>Email</th>
            <th>Enrolled</th>
            <th>Delete</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="student in students" :key="student.id">
            <td>{{ student.id }}</td>
            <td>{{ student.name }}</td>
            <td>{{ student.age }}</td>
            <td>{{ student.major }}</td>
            <td>{{ student.gpa }}</td>
            <td>{{ student.email }}</td>
            <td :class="student.enrolled ? 'enrolled' : 'not-enrolled'">{{ student.enrolled ? "Yes" : "No" }}</td>
            <td><button @click="deleteStudent(student.id)">Delete</button></td>
          </tr>
        </tbody>
    </table>
    
  </div>
</template>

<script>
import {students} from "../mockData";
export default {
  name: "DataList",
  data() {
    return {
      students: students,
    };
  },
  methods: {
    addStudent(formData) {
      const newStudent = {
        id: students.length + 1,
        ...formData,
      };
      this.students.push(newStudent);
      console.log(this.students);
    },
    deleteStudent(id) {
      this.students = this.students.filter((student) => student.id !== id);
    },
    editStudent(id) {
      const student = this.students.find((student) => student.id === id);
      console.log(student);
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  margin-bottom: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin: 0 auto;
  font-family: Arial, sans-serif;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

th {
  background-color: #f2f2f2;
  color: #333;
}

tr:nth-child(even) {
  background-color: #f9f9f9;
}

tr:hover {
  background-color: #f1f1f1;
}
.enrolled {
  color: green;
}
.not-enrolled {
  color: red;
}
</style>

