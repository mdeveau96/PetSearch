<script setup lang="ts">
import { ref } from "vue";
import Menu from 'primevue/menu';

const items = ref([
    {
        label: 'New',
        icon: 'pi pi-plus',
    }
]);
</script>

<template>
    <div class="card flex justify-center p-4">
        <Menu :model="items" class="bg-transparent border-0"/>
    </div>
</template>