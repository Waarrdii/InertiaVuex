<template>
    <div class="flex flex-start">
        <div class="mr-4">
            <Link :href="route('products.index')">Products</Link>
        </div>
        <div class="flex-1">
            <slot name="header"></slot>
            <slot name="content"></slot>
        </div>
    </div>
</template>

<script setup>
import { Link } from '@inertiajs/vue3';



</script>

<style lang="scss" scoped></style>