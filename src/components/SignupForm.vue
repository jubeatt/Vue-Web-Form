<template>
  <form @submit.prevent="onSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <div class="input-field">
      <input :type="inputType" required v-model="password" />
      <FontAwesomeIcon
        @click="onChangeType"
        :icon="inputType === 'text' ? ['fas', 'eye'] : ['fas', 'eye-slash']"
      />
    </div>
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="" disabled hidden>Choose one</option>
      <option value="designer">Web designer</option>
      <option value="developer">Web developer</option>
    </select>

    <label>Skills:</label>
    <input
      type="text"
      placeholder='Press "ctrl + ," to add skill '
      v-model="input"
      @keyup.ctrl="onAddSkill"
    />
    <span class="pill" v-for="skill in skills" :key="skill">
      {{ skill }} <FontAwesomeIcon @click="onRemoveSkill(skill)" :icon="['fas', 'times']" />
    </span>

    <div class="terms">
      <input id="terms" type="checkbox" v-model="terms" required />
      <label for="terms">Terms Accepted:</label>
    </div>

    <div class="submit">
      <button>submit</button>
    </div>
  </form>
  <div class="real-time-data">
    <h3>RealTime-Data</h3>
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role ? role : 'Not choose yet' }}</p>
    <p>Terms accepted: {{ terms ? 'Yes' : 'No' }}</p>
    <p>Skills: {{ skills }}</p>
  </div>
</template>

<script>
export default {
  mounted() {
    document.addEventListener('keydown', (e) => e.key === 'Enter' && e.preventDefault(), true)
  },
  data() {
    return {
      // form data
      email: '',
      password: '',
      role: '',
      terms: false,
      skills: [],
      // state
      input: '',
      passwordError: null,
      inputType: 'password'
    }
  },
  methods: {
    onChangeType() {
      this.inputType = this.inputType === 'password' ? 'text' : 'password'
    },
    onAddSkill(e) {
      const value = this.input.split(',')[0]
      if (e.key === ',' && value && !this.skills.includes(value)) {
        this.skills = [...this.skills, value]
      }
      this.input = ''
    },
    onRemoveSkill(skill) {
      this.skills = this.skills.filter((s) => s !== skill)
    },
    onSubmit() {
      this.passwordError = this.password.length < 5 ? 'Password must be at least 6 char' : null
      if (!this.passwordError) {
        console.log(this.email, this.password, this.role, this.terms, this.skills)
      }
    }
  }
}
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
  font-size: 1em;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
input[type='checkbox'] {
  display: inline-block;
  width: auto;
  margin-right: 1em;
  vertical-align: middle;
}
.input-field {
  display: flex;
  align-items: center;
  gap: 10px;
}
.input-field input {
  flex: 1;
}
.input-field span {
  flex-shrink: 0;
}
.input-field svg {
  cursor: pointer;
}
.input-field svg:hover path {
  color: #333;
}
.input-field svg path {
  color: #aaa;
}
.pill {
  display: inline-flex;
  align-items: center;
  gap: 10px;
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
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
.real-time-data {
  box-sizing: border-box;
  max-width: 250px;
  overflow-x: auto;
  position: fixed;
  bottom: 20px;
  right: 15px;
  padding: 20px;
  background: white;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 15px;
  color: #666;
  align-items: flex-start;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
}
.real-time-data h3 {
  margin: 0;
  margin-bottom: 20px;
}
.real-time-data p {
  white-space: nowrap;
  margin: 0;
}
</style>
