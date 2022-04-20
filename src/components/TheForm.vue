<template>
  <form @submit.prevent="submitForm" :class="{ darkMode: this.darkMode }">
    <button type="button" @click="toggleDarkMode">{{ btnText }}</button>
    <div
      class="form-control"
      :class="{ invalid: this.validName === 'invalid' }"
    >
      <label for="user-name">Your Name</label>
      <input
        id="user-name"
        name="user-name"
        type="text"
        v-model.trim="name"
        @blur="validateName"
      />
      <p v-if="validName === 'invalid'">Please enter a valid name</p>
    </div>
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <!-- Force number convertion -->
      <input
        id="age"
        name="age"
        type="number"
        v-model.number="age"
        ref="ageInput"
      />
    </div>
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select id="referrer" name="referrer" v-model="refer">
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <!-- We need a value attribute to identify specific checkbox -->
        <input
          id="interest-news"
          name="interest"
          value="news"
          type="checkbox"
          v-model="interest"
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
          id="interest-tutorials"
          name="interest"
          value="tutorial"
          type="checkbox"
          v-model="interest"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
          id="interest-nothing"
          name="interest"
          value="nothing"
          type="checkbox"
          v-model="interest"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input
          id="how-video"
          name="how"
          type="radio"
          value="video"
          v-model="how"
        />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input
          id="how-blogs"
          name="how"
          type="radio"
          value="blogs"
          v-model="how"
        />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input
          id="how-other"
          name="how"
          type="radio"
          value="other"
          v-model="how"
        />
        <label for="how-other">Other</label>
      </div>
    </div>
    <div class="form-control">
      <rate-control v-model="score"></rate-control>
    </div>
    <div class="form-control">
      <input
        type="checkbox"
        value="confirm"
        label="confirm"
        name="confirm"
        v-model="confirmAcknowledgement"
      />
      <label for="confirm">Please confirm the user acknowledgement</label>
    </div>

    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>
<script>
import RateControl from './RateControl.vue';
export default {
  components: { RateControl },
  emits: ['darkMode'],
  data() {
    return {
      darkMode: false,
      name: '',
      age: null,
      //Set default value
      refer: 'google',
      // Need to set to [] since we can select multiple value
      interest: [],
      how: null,
      confirmAcknowledgement: false,
      validName: 'pending',
      score: null,
      btnText: 'Dark Mode',
    };
  },
  methods: {
    submitForm() {
      console.log('submitForm', this.name);
      this.name = '';
      // Black means type of string while blue means type of number
      // Common bug that you think you are working with number instead of string
      console.log('Age');
      console.log(this.age);
      console.log(this.$refs.ageInput.value);
      console.log(31);
      this.age = null;
      // For dropdown
      console.log('Dropdown');
      console.log(this.refer);
      this.refer = 'google';
      // For checkbox
      console.log('Checkbox?');
      console.log(this.interest);
      this.interest = [];
      // For radio
      console.log('radio?');
      console.log(this.how);
      this.how = null;
      // For confirm
      console.log('confirm?');
      console.log(this.confirmAcknowledgement);
      this.confirmAcknowledgement = false;
      console.log('Rating');
      console.log(this.score);
      this.score = null;
    },
    validateName() {
      if (this.name === '') {
        this.validName = 'invalid';
        //alert(this.validName);
      } else {
        this.validName = 'valid';
      }
    },
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
      if (this.darkMode) {
        this.btnText = 'Light Mode';
      } else this.btnText = 'Dark Mode';
      this.$emit('darkMode', this.darkMode);
    },
  },
};
</script>
<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}
.darkMode {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #292929;
  color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label {
  color: red;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>
