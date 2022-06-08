<template>
  <div>
    {{ text }}
    {{ number }}
    {{ isHappy }}
    <h1>
      Data Binding
    </h1>
    <button :disabled="isDisabled">
      You can not press me
    </button>
    <div v-bind="objectOfAttrs">
      Text
    </div>
    <h1>
      Javascript Expressions
    </h1>
    <p>
      {{ number + 1 }}
    </p>
     <p>
      {{ number > 10 ? 'The number is bigger than 10' : number === 10 ? 'The number is equal with 10': 'The number is smaller than 10' }}
    </p>
    <p>
      {{ message.split('').reverse().join('') }}
    </p>
    <h1>
      Style bindings
    </h1>
    <div :id="`test-${id}`">
      Here is a div with a binded id
    </div>
    <h1>
      Reactivity and functions
    </h1>
    <p>
      {{ number }}
    </p>
    <button @click="number++">
      Press me to increment number
    </button>
    <button @click="number--">
      Press me to decrement number
    </button>
    <button @click="increment">
      Press me to increment number
    </button>
    <button @click="decrement">
      Press me to decrement number
    </button>
     <button @click="incrementByNumber(5)">
      Press me to increment by specified number
    </button>
    <button @click="decrementByNumber(10)">
      Press me to decrement by specified number
    </button>
    <div v-if="number < 10" class="box red" />
    <div v-else-if="number === 10" class="box blue" />
    <div v-else class="box green" />
    <div v-show="number < 10" class="box red" />
    <div v-html="html" />
    <h1>
      Computed
    </h1>
    <p>
      Without computed {{ number > 5 ? 'Number is bigger than 5' : number === 5 ? 'Number is equal to 5' : 'Number is less than 5' }}
    </p>
    <p>
      With computed {{ getNumberState }}
    </p>
    <h1>
      List rendering
    </h1>
    <ul>
      <li>
        Denis
      </li>
      <li>
        George
      </li>
      <li>
        Mathew
      </li>
    </ul>
    <ul>
      <li v-for="friend in friends" :key="friend">
        {{ friend }}
      </li>
    </ul>
    <h1>
      Form Input Bindings
    </h1>
    <p>
      Input text is: {{ formData.inputText }}
    </p>
    <input type="text" v-model="formData.inputText">
    <p>
      Textarea text is {{ formData.textareaText }}
    </p>
    <textarea v-model="formData.textareaText"></textarea>
    <input type="checkbox" id="checkbox" v-model="formData.checked" />
    <label for="checkbox">{{ formData.checked }}</label>
    <p>
      Invited Friend: {{ formData.invitedFriends }}
    </p>
    <input type="checkbox" value="Denis" id="denis" v-model="formData.invitedFriends">
    <label for="denis">Denis</label>
    <input type="checkbox" value="John" v-model="formData.invitedFriends">
    <label for="john">John</label>
    <input type="checkbox" value="Mathew" v-model="formData.invitedFriends">
    <label for="mathew">Mathew</label>
    <p>
      Picked: {{ formData.picked }}
    </p>
    <input type="radio" id="one" value="One" v-model="formData.picked">
    <label for="one">One</label>
    <input type="radio" id="two" value="Two" v-model="formData.picked">
    <label for="two">Two</label>
    <p>
     Selected: {{ formData.selected }}
   </p>
   <select v-model="formData.selected">
     <option disabled value="">Please select one option</option>
     <option>A</option>
     <option>B</option>
     <option>C</option>
   </select>
    <p>
      Form Details {{ formDetails }}
    </p>
    <form @submit.prevent="submitForm">
      <label for="">First Name</label>
      <input type="text" v-model="formDetails.firstName">
      <label for="">Last Name</label>
      <input type="text" v-model="formDetails.lastName">
      <label for="">Description</label>
      <textarea v-model="formDetails.description"></textarea>
      <select v-model="formDetails.gender">
        <option disabled> Please select your gender </option>
        <option>
          Male
        </option>
        <option>
          Female
        </option>
        <option>
          Other
        </option>
      </select>
      <button type="submit">
        Submit
      </button>
    </form>
    <p>
      X value : {{ x }}
    </p>
    <button @click="x++">
      Click to increment X
    </button>
    <h1>
      Template refs
    </h1>
    <input type="text" ref="input">
    <h1>Components</h1>
    <first-component :parent-message="message" parent-number="10" @my-first-emit="getDataFromChild">
      <template #header="slotProps">
        <div>
          Slot header
        </div>
        <p>
          {{ slotProps.number }}
        </p>
      </template>
      <template #footer>
        <div>
          Slot footer
        </div>
      </template>
    </first-component>
  </div>
</template>

<script>
import FirstComponent from './components/FirstComponent';
export default {
  name: 'App',
  components: {
    FirstComponent
  },
  data() {
    return {
      message: 'Hello Child Component',
      text: 'Hello World',
      number: 1,
      isHappy: true,
      isDisabled: true,
      objectOfAttrs: {
        id: 'main',
        class: 'container'
      },
      id: 'container',
      html: '<div class="box green" />',
      friends: ['Denis', 'George', 'Mathew'],
      formData: {
        inputText: '',
        textareaText: '',
        checked: false,
        invitedFriends: [],
        picked: [],
        selected: ''
      },
      formDetails: {
        firstName: '',
        lastName: '',
        description: '',
        gender: '',
      },
      x: 1
    }
  },
  methods: {
    increment() {
      this.number++
      },
    decrement() {
      this.number--
    },
    incrementByNumber(value) {
      this.number = this.number + value;
    },
    decrementByNumber(value) {
      this.number = this.number - value;
    },
    submitForm() {
      console.log(this.formDetails);
    },
    getDataFromChild(data) {
      console.log(data);
    }
  },
  mounted() {
    console.log("The component is mounted");
    this.$refs.input.focus();
  },
  created() {
    console.log("The component is created");
  },
  watch: {
    x(newX, oldX) {
      console.log("old x was " + oldX);
      console.log("new x is " + newX);
    }
  }
}
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
.box {
  width: 50px;
  height: 50px;
}
.red {
  background: red;
}
.blue {
  background: blue;
}
.green {
  background: green;
}
</style>
