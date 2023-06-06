<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input
      type="email"
      required
      v-model="email"
      placeholder="Enter Email here"
    />
    <label>Password:</label>
    <input
      type="password"
      required
      v-model="password"
      placeholder="Enter password here"
    />
    <div class="error" v-if="errorMessage">
      {{errorMessage}}
    </div>
    <label>---Select Role---</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
      <option value="tester">Web Tester</option>
      <option value="presenter">Web Presenter</option>
    </select>
    <label>Skills:</label>
    <input
      type="text"
      placeholder="Add your Skills"
      v-model="tempSkills"
      @keyup.alt="addSkill"
    />

    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>
    <div class="term">
      <input type="checkbox" v-model="term" required />
      <label>Accept terms and conditions</label>
    </div>
    <div class="submit">
      <button>Create new account</button>
    </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Term: {{ term }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      term: false,
      tempSkills: [],
      skills: [],
      errorMessage: ''
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkills) {
        if (!this.skills.includes(this.tempSkills)) {
          this.skills.push(this.tempSkills);
        }
        this.tempSkills = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((ele) => {
        return ele !== skill;
      });
    },
    handleSubmit () {
      this.errorMessage = this.errorMessage.length > 5 ? '': 'Password must be greater than 5 character'
      if(!this.errorMessage){
        console.log('formSubmitted successfully!');
      }
    }
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>