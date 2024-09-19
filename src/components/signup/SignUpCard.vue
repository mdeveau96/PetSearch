<script setup lang="ts">
import { ref } from 'vue'
import Card from 'primevue/card'
import Divider from 'primevue/divider'
import InputText from 'primevue/inputtext'
import Button from 'primevue/button'
import Select from 'primevue/select'
import Message from 'primevue/message'
import Menu from 'primevue/menu'
import { UsCities } from '@/service/uscities'

const countiesList = ref(UsCities.getCitiesData())
const firstname = ref()
const lastname = ref()
const email = ref()
const phone = ref()
const selectedCounty = ref()
const next = ref(0)
const password1 = ref()
const password2 = ref()
const matchPassword = ref()

const menuItems = ref([
  {
    label: 'Back',
    icon: 'pi pi-arrow-left'
  }
])

const confirmedPW = (password1: string, password2: string) => {
  if (password1 === password2) {
    matchPassword.value = true
  } else {
    matchPassword.value = false
  }
}

function createAccount() {
  const data = {
    "first_name": firstname.value,
    "last_name": lastname.value,
    "email": email.value,
    "phone": phone.value,
    "county": selectedCounty.value,
    "password": password1.value
  }
  if (matchPassword.value) {
    console.log(data)
  }
  // TODO - push data for future database to house users (maybe Cognito user pool)
}
</script>

<template>
  <Card v-if="next===0" style="width: 25rem; overflow: hidden" class="mx-auto border border-surface-800 shadow">
    <template #title><h1 class="font-bold">Welcome!</h1></template>
    <template #content>
      <p>
        If you already have account
        <router-link to="/login" class="text-blue-600 hover:underline">log in</router-link>!
      </p>
      <div class="grid grid-cols-1 gap-4">
        <Divider />
        <div>
          <label for="firstname">First Name</label>
          <InputText v-model="firstname" id="firstname" class="w-full" placeholder="First Name" />
        </div>
        <div>
          <label for="lastname">Last Name</label>
          <InputText v-model="lastname" id="lastname" class="w-full" placeholder="Last Name" />
        </div>
        <div>
          <label for="email">Email</label>
          <InputText v-model="email" id="email" class="w-full" placeholder="Email" />
        </div>
        <div>
          <label for="phone">Phone</label>
          <InputText v-model="phone" id="phone" class="w-full" placeholder="Phone" />
        </div>
        <div>
          <label for="location">Select a County</label>
          <Select v-model="selectedCounty" filter :options="countiesList" optionLabel="county_name" placeholder="Select a County" class="w-full" />
        </div>
        <div>
          <Button type="submit" class="bg-sky-500 border-0 hover:bg-sky-600 w-full" @click="next++">Next</Button>
        </div>
      </div>
    </template>
  </Card>
  <div v-if="next===1" class="card flex justify-center">
    <Menu :model="menuItems" class="bg-transparent border-0 px-4">
      <template #item="{ item, props }">
        <a class="flex items-center" v-bind="props.action" @click="next--">
          <span :class="item.icon" />
          <span>{{ item.label }}</span>
        </a>
      </template>
    </Menu>
    <Card style="width: 25rem; overflow: hidden" class="border border-surface-800 shadow">
      <template #title><h1 class="font-bold">Create your password</h1></template>
      <template #content>
        <div class="grid grid-cols-1 gap-4">
          <Divider />
          <div v-if="matchPassword==false">
            <Message severity="error">Passwords do not match!</Message>
          </div>
          <div>
            <label for="phone">Password</label>
            <InputText v-model="password1" id="password1" class="w-full" placeholder="Password" type="password"/>
          </div>
          <div>
            <label for="location">Confirm Password</label>
            <InputText v-model="password2" id="password2" class="w-full" placeholder="Confirm Password" type="password"/>
          </div>
          <div>
            <Button type="submit" class="bg-sky-500 border-0 hover:bg-sky-600 w-full" 
            @click="confirmedPW(password1, password2), createAccount()">Create Account</Button>
          </div>
        </div>
      </template>
    </Card>
  </div>
</template>
