<script setup>
import { onMounted, provide, reactive } from 'vue'
import { Link } from '@inertiajs/vue3';

import Welcome from '../Welcome.vue';

const props = defineProps({
    products: Array,
})

const activeTab = reactive([]);

onMounted(() => {
    activeTab.push({
        id: 'index',
        active: true
    })
})

const openTab = (tabName) => {
    const existTab = activeTab.findIndex(tab => tab.id === tabName);
    if (existTab === -1) {
        activeTab.push({
            id: tabName,
            active: true
        })
    } else {
        activeTab[existTab].active = true;
    }
}

</script>


<template>
    <Welcome>
        <template #header>
            <div class="flex space-x-2 mb-4">
                <div v-for="tab in activeTab" :key="tab.id"
                    :class="[tab.active ? 'bg-gray-200' : 'bg-gray-100']"
                    class="first:rounded-tl-md last:rounded-tr-md border-r bg-gray-100 p-2 hover:bg-gray-200 cursor-pointer ">
                    <Link :href="route(`products.${tab.id}`)"
                    class="uppercase cursor-pointer">{{ tab.id }}</Link>
                </div>
            </div>

        </template>
        <template #content>
            <div>
                <div v-for="product in products" :key="product.id">
                    {{ product.name }}
                </div>

                <Link :href="route('products.create')" @click="openTab('create')">Create</Link>
            </div>
        </template>
    </Welcome>
</template>