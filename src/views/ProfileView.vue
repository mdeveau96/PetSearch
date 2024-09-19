<script setup lang="ts">
import { useRoute } from 'vue-router';
import ProfileCard from '@/components/profile/ProfileCard.vue';
import { computed } from 'vue';
import sourceTestData from '@/data.json'
const route = useRoute();
const userId = computed(() => {
    return parseInt(route.params.user_id as string)
})

const user = computed(() => {
    return sourceTestData.users.find(user => user.user_id === userId.value)
})
</script>

<template>
    <div>
        <!-- <ProfileCard /> -->
        First name: {{ user?.first_name }}
        Last name: {{ user?.last_name }}
        email: {{ user?.email }}
        phone: {{ user?.phone }}
        county: {{ user?.county }}
    </div>
</template>