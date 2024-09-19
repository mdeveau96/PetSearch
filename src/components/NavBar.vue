<script setup lang="ts">
import InputText from 'primevue/inputtext';
import Menubar from 'primevue/menubar'
import IconField from 'primevue/iconfield';
import InputIcon from 'primevue/inputicon';
import { ref } from "vue";

const items = ref([
    {
        label: 'About',
        route: '/about'
    },
    {
        label: 'Groups',
        route: '/groups'
    }
]);
</script>

<template>
    <Menubar :model="items" class="py-2">
        <template #start>
            <div class="mx-4">
                <router-link to="/"><svg width="40" height="40" viewBox="0 0 40 40" fill="none" class="bg-gray-600 rounded-full"></svg></router-link>
            </div>
        </template>
        <template #item="{ item, props }">
            <router-link v-if="item.route" v-slot="{ href, navigate }" :to="item.route">
                <div class="hover:bg-surface-700 rounded-full">
                    <a :href="href" v-bind="props.action" @click="navigate">
                        <span class="font-semibold">{{ item.label }}</span>
                    </a>
                </div>
            </router-link>
            <a v-else v-ripple class="flex items-center" v-bind="props.action">
                <span :class="item.icon" />
                <span class="ml-2">{{ item.label }}</span>
            </a>
        </template>
        <template #end>
            <div class="flex items-center gap-4 mx-4">
                <IconField>
                    <InputIcon class="pi pi-search px-2" />
                    <InputText placeholder="Search..." class="focus:w-96 rounded-full"/>
                </IconField>
                <router-link to="/login"><Button class="hover:bg-surface-700 font-semibold px-4 py-2.5 rounded-full">Log in</Button></router-link>
                <router-link to="/signup"><Button class="bg-black font-semibold text-white px-4 py-2.5 rounded-full hover:bg-white hover:text-black">Sign Up</Button></router-link>
                <router-link to="/profile">
                    <div class="h-12 w-12 bg-gray-600 rounded-full">
                        <!-- <Avatar shape="circle"/> -->
                    </div>
                </router-link>
            </div>
        </template>
    </Menubar>
</template>
