<script>
import { walkBlockDeclarations } from '@vue/compiler-core';

export default {
        data() {
                return {
                        items: [],
                }
        },
        methods: {
                async getData() {
                        const apiFetch = await fetch("https://raw.githubusercontent.com/ironhack-jc/mid-term-api/main/cart");
                        const apiData = await apiFetch.json();
                        this.items = apiData;
                },
        },
        mounted() {
                this.getData();
        }
}

</script>

<template>
        <h1 class="font-bold text-2xl m-2 px-5">Shopping Cart</h1>
        <table class="m-2 py-5">
                <thead class="p-2">
                        <tr>
                                <th class="p-4">Product</th>
                                <th class="p-4">Price</th>
                                <th class="p-4">Quantity</th>
                                <th class="p-4">Subtotal</th>
                                <th class="p-4"></th>
                        </tr>
                </thead>
                <tbody class="p-2">
                        <tr>
                                <td class="px-4">{{ items[0].name }}</td>
                                <td class="px-4">EUR</td>
                                <td class="px-4"></td>
                                <td class="px-4">$$$</td>
                                <td class="px-4"></td>
                        </tr>
                </tbody>
        </table>
</template>

<style scoped>

</style>
