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
        computed: {

        },
        mounted() {
                this.getData();
        }
}

</script>

<template>
        <nav class="h-20 px-4 flex justify-between items-center whitespace-nowrap">
                <div class="flex items-center">
                        <div class="min-w-[4rem]">
                                <img src="./assets/4185501-freepik-objlogo.png" class="h-12 px-2" />
                        </div>
                        <div class="font-bold text-center text-3xl text-cyan-600 small-caps">vuest deals</div>
                </div>
                <ul class="flex items-center justify-around px-10">
                        <li class="px-5">Products</li>
                        <li class="px-5">Sales</li>
                        <li class="px-5">About Us</li>
                </ul>
                <div class="flex items-center">
                        <div class="min-w-[4rem]">
                                <img src="./assets/1077897-freepik-cartlogo.png" class="h-8 px-2" />
                        </div>
                        <div class="text-cyan-700 small-caps">( 1 )</div>
                </div>
        </nav>

        <div>
                <div>
                        <h1 class="font-bold text-xl px-20 mt-8 mb-8 text-cyan-700 small-caps">Shopping Cart</h1>
                </div>
                <table class="mt-2 mx-auto py-10">
                        <thead class="p-2 text-cyan-600">
                                <tr>
                                        <th class="p-4 w-20"></th>
                                        <th class="p-4 w-60 text-left">Product</th>
                                        <th class="p-4 w-40">Price</th>
                                        <th class="p-4 w-40">Quantity</th>
                                        <th class="p-4 w-40">Subtotal</th>

                                </tr>
                        </thead>
                        <tbody class="p-2">
                                <tr v-for="item in items" class="">
                                        <td class="px-4 flex justify-center min-w-[4.5rem]"><img :src="item.image"
                                                        :alt="item.name" class="h-10 w-10 rounded-full" /></td>
                                        <td class="px-4">{{ item.name }}</td>
                                        <td class="px-4 text-right">{{ item.price }} EUR</td>
                                        <td class="px-4">
                                                <input type="number" placeholder="0" class="w-20 border" />
                                        </td>
                                        <td class="px-4">nnn</td>
                                </tr>
                        </tbody>
                </table>
        </div>
        <footer>
                
        </footer>

</template>

<style scoped>
.small-caps {
        font-variant-caps: all-small-caps;
}
</style>
