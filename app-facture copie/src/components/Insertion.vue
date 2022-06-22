<script setup lang="ts">
import WelcomeItem from './Item.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
</script>

<template>
  <div id="app">
  <form @submit.prevent="submitForm" autocomplete="off">
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>User ID</template>

    Veuillez entrer l'ID du client pour qui la facture va être generer.

<br/>

    <p>L'userID est : {{ form.userID }}</p>
    <p>
      <label for="userID">userID</label>
      <input
          id="userID"
          v-model="form.userID"
          type="number"
          name="userID"
      >
    </p>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <ToolingIcon />
    </template>
    <template #heading>Date de Début</template>

    Veuillez entrer la date de début de la Facture.

    <br />

    <p>La date de début est : {{ form.startDate }}</p>
    <p>
      <label for="startDate">startDate</label>
      <input
          id="startDate"
          v-model="form.startDate"
          type="date"
          name="startDate"
      >
    </p>
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <EcosystemIcon />
    </template>
    <template #heading>Date de Fin</template>

    Veuillez entrer la date de Fin de la Facture.

    <br />

    <p>La date de fin est : {{ form.endDate }}</p>
    <p>
      <label for="endDate">endDate</label>
      <input
          id="endDate"
          v-model="form.endDate"
          type="date"
          name="endDate"
      >
    </p>

  </WelcomeItem>

  <div>
    <button>Submit</button>
  </div>
  </form>
  </div>

</template>

<script lang="ts">
import Axios from 'axios'

export default {
  el: '#app',

  data() {
    return {
      form: {
        userID: null,
        startDate: null,
        endDate: null
      }
    }
  },

  methods: {
    submitForm() {
      const userIsValid = typeof this.form.userID ==='number'
      if (userIsValid) {
        Axios.post('http://localhost:8081/account/invoices/newinvoices', this.form).then((page)=>console.log(page))
        console.log('Form Submitted', this.form)
      }else {
        console.log('Form is Invalid')
      }

    }
  }
}
</script>
