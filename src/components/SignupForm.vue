<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="text" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role" required>
      <option value="developer">Web developer</option>
      <option value="designer">Web designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
    <div v-for="skill in skills" :key="skill" class="skill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="cheboxField">
      <input type="checkbox" id="terms" required v-model="terms" />
      <label for="terms">Accept terms</label>
    </div>

    <div class="cheboxField">
      <input type="checkbox" id="first" value="first" v-model="conditions" />
      <label for="first">Accept first condition</label>
    </div>
    <div class="cheboxField">
      <input type="checkbox" id="second" value="second" v-model="conditions" />
      <label for="second">Accept second condition</label>
    </div>
    <div class="cheboxField">
      <input type="checkbox" id="third" value="third" v-model="conditions" />
      <label for="third">Accept third condition</label>
    </div>

    <div class="submit">
      <button type="submit">Submit</button>
    </div>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
  <p>Conditions {{ conditions }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      conditions: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (
        e.key === "," &&
        this.tempSkill &&
        !this.skills.includes(this.tempSkill)
      ) {
        this.skills.push(this.tempSkill);
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => item !== skill);
    },
    handleSubmit() {
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 characters long";

      console.log("email:", this.email);
      console.log("password:", this.password);
      console.log("role:", this.role);
      console.log("skills:", this.skills);
      console.log("terms:", this.terms);
      console.log("conditions:", this.conditions);
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: #fff;
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
.cheboxField label {
  margin: 15px 0 0;
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
.skill {
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
  color: #fff;
  border-radius: 20px;
  cursor: pointer;
}
.submit {
  text-align: center;
}
.error {
}
</style>
