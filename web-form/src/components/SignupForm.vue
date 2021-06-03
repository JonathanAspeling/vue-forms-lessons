<template>
  <div>
    <form>
      <label>Email:</label>
      <input type="email" required v-model="email" />
      <label>Password:</label>
      <input type="password" required v-model="password" />
      <label>Role:</label>
      <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>
      <label>Skills</label>
      <input
        type="text"
        name=""
        id=""
        v-model="tempSkill"
        @keyup.alt="addSkill"
      />
      <div
        v-for="skill in skills"
        :key="skill"
        class="pill"
        @click="removeSkill(skill)"
      >
        {{ skill }}
      </div>

      <div class="terms">
        <input type="checkbox" required v-model="terms" />
        <label>Accept Terms and Conditions.</label>
      </div>
    </form>
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p v-if="terms">Terms Accepted</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
    };
  },
  methods: {
    addSkill(event) {
      if (event.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
      console.log(this.skills);
    },
    removeSkill(skill) {
      delete this.skills[this.getKeyByValue(this.skills, skill)];
      this.skills = this.skills;
      console.log(this.skills);
    },
    getKeyByValue(array, value) {
      return Object.keys(array).find((key) => array[key] === value);
    },
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
  font-size: 0.6em;
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
  background: #680;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #eee;
  cursor: pointer;
}
</style>