<template>
  <v-card class="mx-auto my-10 bg-blue-grey-darken-4" max-width="500" theme="dark">
    <v-card-title class="text-h6 font-weight-regular justify-space-between">
      <span>{{ currentTitle }}</span>
      <v-avatar color="primary" size="24">{{ step }}</v-avatar>
    </v-card-title>

    <v-window v-model="step">
      <v-window-item :value="1">
        <v-card-text>
          <v-text-field
            id="username"
            name="username"
            label="Usename"
            type="text"
            placeholder="Usename"
            v-model="enteredUsername"
            :rules="rules2"
          ></v-text-field>
          <span class="text-caption text-grey">
            please enter your username.
          </span>
        </v-card-text>
      </v-window-item>

      <v-window-item :value="2">
        <v-card-text>
          <v-text-field
            id="email"
            name="email"
            label="email"
            type="text"
            placeholder="test@gmail.com"
            v-model="enteredEmail"
            :rules="rules"
          ></v-text-field>
          <span class="text-caption text-grey">
            please enter your E-mail.
          </span>
        </v-card-text>
      </v-window-item>

      <v-window-item :value="3">
        <div class="pa-4 text-center">
          <p><span class="text-grey">your username: </span>{{ enteredUsername }}</p>
          <p><span class="text-grey">your E-mail: </span>{{ enteredEmail }}</p>

        </div>
      </v-window-item>
    </v-window>

    <v-divider></v-divider>

    <v-card-actions>
      <v-btn v-if="step > 1" variant="text" @click="step--" id="btn-prev"> Back </v-btn>
      <v-spacer></v-spacer>
      <v-btn v-if="step < 3" color="primary" variant="flat" @click="step++" id="btn-next">
        Next
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { computed, ref } from "vue";

const step = ref(1);
const enteredUsername = ref("");
const enteredEmail = ref("");

const currentTitle = computed(() => {
  switch (step.value) {
    case 1:
      return "Username";
    case 2:
      return "Email";
    default:
      return "review";
  }
});

const rules = [
    value => !!value || 'Required.',
    value => (value || '').length <= 20 || 'Max 20 characters',
    value => {
      const pattern =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      return pattern.test(value) || 'Invalid e-mail.'
    },
  ]

  const rules2 = [
    value => !!value || 'Required.',
    value => (value && value.length >= 3) || 'Min 3 characters',
  ]
</script>
