<template>
  <div>
    <form v-on:submit.prevent="handleSubmit">
      <div class="field">
        <label class="label">Name</label>
        <div class="control">
          <input
            v-model="form.name"
            class="input"
            type="text"
            placeholder="Text input"
          />
        </div>
      </div>
      <div class="field">
        <textarea
          class="textarea"
          placeholder="Message"
          v-model="form.message"
        ></textarea>
      </div>
      <div>
        <select v-model="form.inquiry_type">
          <option disabled value="">Nothing selected</option>
          <option
            v-for="(option, i) in options.inquiry"
            :key="i"
            v-bind:value="option.value"
          >
            {{ option.text }}
          </option>
        </select>
      </div>
      <div>
        <select multiple v-model="form.usecases">
          <option>Debugging</option>
          <option>Fixing Errors</option>
          <option>User support</option>
        </select>
      </div>
      <div>
        <label class="checkbox">
          <input type="checkbox" v-model="form.terms" />
          I agree to the <a href="#">terms and conditions</a>
        </label>
      </div>
      <div class="control">
        <label class="checkbox">
          <input type="checkbox" v-model="form.concepts" value="promises" />
          Promises
        </label>
        <label class="checkbox">
          <input type="checkbox" v-model="form.concepts" value="testing" />
          Testing
        </label>
      </div>
      <div class="control">
        <label class="radio">
          <input v-model="form.js_awesome" type="radio" value="Yes" />
          Yes
        </label>
        <label class="radio">
          <input v-model="form.js_awesome" type="radio" value="Yeap!" />
          Yeap!
        </label>
      </div>
      <div class="field is-grouped">
        <div class="control">
          <button class="button is-primary">Submit</button>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
// import ExampleAnalyticsService from "./example-analytics-service";
export default {
  data() {
    return {
      form: {
        name: "",
        message: "",
        inquiry_type: "",
        usecases: [],
        terms: false,
        concepts: [],
        js_awesome: "", // nilai radio input
      },
      options: {
        inquiry: [
          { value: "feature", text: "Feature Request" },
          { value: "bug", text: "Bug Report" },
          { value: "support", text: "Support" },
        ],
      },
    };
  },
  methods: {
    handleSubmit() {
      console.log(this.form);
    },
  },
};
</script>
