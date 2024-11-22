<script setup>
import TextInput from '@/Components/TextInput.vue';
import InputLabel from '@/Components/InputLabel.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import { router, useForm } from '@inertiajs/vue3';
import Welcome from '../Welcome.vue';
import { reactive, onMounted } from 'vue';

const activeTab = reactive([]);

onMounted(() => {
  // Menambahkan tab 'index' dengan status active false
  activeTab.push({
    id: 'index',
    active: false
  });

  // Menambahkan tab 'create' dengan status active true
  activeTab.push({
    id: 'create',
    active: true
  });
  console.log(activeTab);
});


const submit = () => {
    router.post('/products', form)
}

const form = useForm({
    'name': ''
})
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
            <form @submit.prevent="submit">
                <InputLabel for="name" value="Name" />
                <TextInput id="name" type="text" class="mt-1 block w-40" v-model="form.name">
                    Name
                </TextInput>

                <SecondaryButton type="submit">Save</SecondaryButton>

            </form>
        </template>
    </Welcome>

</template>


<style lang="scss" scoped></style>