<template>
  <form @submit.prevent="handleSubmit">
    <label>Email :</label>
    <input type="email" required v-model="email" placeholder="Your email address" />

    <label>Password :</label>
    <input type="password" required v-model="password" placeholder="Your Password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" placeholder="Enter any your skills ended by comma (,)" />
    <div v-for="(skill, index) in skills" :key="skill" class="pill" @click="removeSkill(index)">
      {{ skill }}
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill !== ",") {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill.replace(/.$/, ""));
        }
        this.tempSkill = "";
      }
    },
    removeSkill(index) {
      this.skills.splice(index, 1);
    },
    handleSubmit() {
      // validate password
      this.passwordError = this.password.length > 5 ? "" : "Password must be at least 6 chars long";
      if (!this.passwordError) {
        console.log("email", this.email);
      }
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
  background: white;
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input:focus {
  outline: none;
  border-bottom: 2px solid rgb(202, 246, 246);
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

input::placeholder {
  color: rgb(210, 210, 210);
  font-size: small;
}
button {
  background: #0b7dff;
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
  color: #ff0062aa;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
