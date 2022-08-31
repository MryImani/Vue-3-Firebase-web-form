<template>
  <form @submit.prevent="handelSubmit">
    <label>Email:</label>
    <input type="text" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>role:</label>
    <select v-model="role">
      <option value="choose">Choose</option>
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
      <option value="developer">Data Analysit</option>
    </select>

    <label>skills:</label>
    <input type="text" v-model="tempSkills" @keyup="addSkill" />

    <div class="skills" v-if="skills">
      <span
        class="skill"
        v-for="skill in skills"
        :key="skill"
        @click="removeSkill(skill)"
        >{{ skill }}</span
      >
    </div>

    <div class="terms">
      <input type="checkbox" required />
      <label>Accept Terms And Condition </label>
    </div>
    <div class="submit">
      <button>Create An Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "choose",
      terms: false,
      tempSkills: [],
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (
        (e.key === "," || e.key === "-" || e.key === " ") &&
        this.tempSkills
      ) {
        let tempskill = this.tempSkills;
        let skill = tempskill.substr(0, tempskill.length - 1);
        if (!this.skills.includes(skill)) {
          this.skills.push(skill);
        }
        this.tempSkills = "";
      }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handelSubmit() {
      let data = {
        email: this.email,
        password: this.password,
        role: this.role,
        skills: this.skills,
        terms: this.terms,
      };
      //check password validation
      this.passwordError =
        this.password.length > 5
          ? ""
          : "* Password must be at least 6 char  or long";
      if (!this.passwordError) {
        console.log(data);
      }
    },
  },
};
</script>

<style>
form {
  max-width: 26.25rem;
  margin: 1.875rem auto;
  background: #fff;
  text-align: left;
  padding: 2.5rem;
  border-radius: 0.625rem;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 1.562rem 0 0.937rem;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 0.625rem 0.375rem;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 1rem;
  margin: 0 0.625rem 0 0;
  position: relative;
  top: 2px;
}
.skills {
  margin: 1.562rem 0 0.937rem;
}
.skill {
  margin-right: 15px;
  padding: 10px;
  background: #eee;
  border-radius: 5px;
  text-align: center;
  font-weight: bold;
  font-size: 12px;
  cursor: pointer;
  color: #777;
  letter-spacing: 1px;
}
.submit {
  text-align: center;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: #fff;
  border-radius: 20px;
}
.error {
  color: #f00;
  font-size: 0.8rem;
  font-weight: bold;
  padding: 5px;
}
</style>