<script setup lang="ts">
import { ref } from 'vue'
import Card from 'primevue/card';
import Divider from 'primevue/divider';
import InputText from 'primevue/inputtext';
import Button from 'primevue/button';
import Message from 'primevue/message';

const email = ref(null)
const password = ref(null)
const successfulMatch = ref()

function login() {
    const data = {
        "email": email.value,
        "password": password.value
    }
    console.log(data)
    // TODO send request to user lookup to match credentials
    successfulMatch.value = false
}
</script>

<template>
    <Card style="width: 25rem; overflow: hidden" class="mx-auto border border-surface-800 shadow">
        <template #title><h1 class="font-bold">Log In</h1></template>
        <template #content>
            <p>
                Don't have an account? Sign up <router-link to="/signup" class="text-blue-600 hover:underline">here</router-link>!
            </p>
            <div class="grid grid-cols-1 gap-4">
                <Divider/>
                <div v-if="successfulMatch==false">
                    <Message severity="error">Invalid email/password</Message>
                </div>
                <div>
                    <label for="email">Email</label>
                    <InputText v-model="email" id="email" class="w-full" placeholder="Email" />
                </div>
                <div>
                    <label for="password">Password</label>
                    <InputText v-model="password" id="password" class="w-full" placeholder="Password" type="password" />
                </div>
                <div>
                    <Button type="submit" class="bg-sky-500 border-0 hover:bg-sky-600 w-full" 
                    @click="login()">Log In</Button>
                </div>
            </div>
        </template>
    </Card>
</template>