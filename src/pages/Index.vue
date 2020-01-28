<template>
  <q-page padding>
    <button
      style="position: absolute; right: 10px"
      @click = "counter++"
    >
      {{counter}}
    </button>
    <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      :class="{'error' : message.length > 20}"
     />
    <button @click="clearMessage"> Clear </button>

    <div > {{ message.length }} / 20  </div>
    <h5
      v-if="message.length"
      class="border-grey">
        {{ message }}
    </h5>
    <h6 v-else >
      No message entered
    </h6>
    <hr>

    <p>Uppercase message: {{ messageUppercase }}</p>
    <hr>
    <p>Lowercase message: {{ message | messageLowerCase }}</p>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      message: 'I love Vue.js',
      counter: 0
    }
  },
  computed: {
    messageUppercase () {
      console.log('messageUppercase was fired')
      return this.message.toUpperCase() + this.counter
    }
  },
  methods: {
    clearMessage () {
      this.message = ''
    },
    alertMessage () {
      alert(this.message)
    }
  },
  filters: {
    messageLowerCase (value) {
      return value.toLowerCase()
    }
  },
  directives: {
    autofocus: {
      inserted (el) {
        el.focus()
      }
    }
  }
}
</script>

<style lang="scss">
  .border-grey {
    border: 1px solid grey;
  }

  input, button {
    font-size: 18px;
  }
  .error {
    color: red;
    background-color: pink;
  }
</style>
