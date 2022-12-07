<script>
import { walkBlockDeclarations } from "@vue/compiler-core";

export default {
        data() {
                return {
                        items: [],
                };
        },
        methods: {
                async getData() {
                        const apiFetch = await fetch(
                                "https://raw.githubusercontent.com/ironhack-jc/mid-term-api/main/cart"
                        );
                        const apiData = await apiFetch.json();
                        this.items = apiData;
                },
                calcSubtotal(item) {
                        this.subtotal = item.quantity * item.price;
                        return this.subtotal;
                },
        },
        computed: {
                sumTotal() {
                        return this.items.reduce(function (sum, item) {
                                return item.price * item.quantity + sum
                        }, 0);
                },
                cartNum() {
                        // return this.items.reduce(function(carry, item){
                        //         return item.quantity += carry
                        // }, 0);
                        let sum = 0;
                        for (const item of this.items) {
                                sum += item.quantity;
                        };
                        return sum;
                },
        },
        mounted() {
                this.getData();
        },
};
</script>

<template>
        <nav class="h-20 px-4 flex justify-between items-center whitespace-nowrap">
                <div class="flex items-center">
                        <div class="min-w-[4rem]">
                                <img src="./assets/4185501-freepik-objlogo.png" class="h-12 px-2" />
                        </div>
                        <div class="font-bold text-center text-3xl text-cyan-600 small-caps">
                                vuest deals
                        </div>
                </div>
                <ul class="flex items-center justify-around px-10 small-caps">
                        <li class="px-5">Products</li>
                        <li class="px-5">Sales</li>
                        <li class="px-5">About Us</li>
                </ul>
                <div class="flex items-center">
                        <div class="min-w-[4rem]">
                                <img src="./assets/1077897-freepik-cartlogo.png" class="h-8 px-2" />
                        </div>
                        <div class="text-cyan-700 small-caps">( {{ cartNum }} )</div>
                </div>
        </nav>

        <div>
                <div>
                        <h1
                                class="font-bold text-xl px-20 mt-8 mb-8 bg-gradient-to-r from-cyan-700 to-cyan-500 text-white small-caps leading-loose">
                                Shopping Cart
                        </h1>
                </div>
                <table class="mt-2 mx-auto py-10 leading-loose">
                        <thead class="p-2 text-cyan-600 small-caps">
                                <tr>
                                        <th class="p-4 w-40"></th>
                                        <th class="p-4 w-60 text-left">
                                                Product
                                        </th>
                                        <th class="p-4 w-40 text-right">
                                                Price
                                        </th>
                                        <th class="p-4 w-40 text-right">
                                                Quantity
                                        </th>
                                        <th class="p-4 w-40 text-right">
                                                Subtotal
                                        </th>
                                        <th class="p-4 w-40"></th>
                                </tr>
                        </thead>
                        <tbody class="p-2">
                                <tr v-for="(item, index) in items" :key="index" class="h-16">
                                        <td class="flex justify-center items-center h-16 min-w-[5.5rem]">
                                                <img :src="item.image" :alt="item.name"
                                                        class="h-14 w-14 rounded-full" />
                                        </td>
                                        <td class="px-4 small-caps font-semibold">
                                                {{ item.name }}
                                        </td>
                                        <td class="px-4 text-right text-sm font-light">
                                                {{ item.price }} €
                                        </td>
                                        <td class="px-4 text-right">
                                                <input type="number" v-model.number="
                                                        item.quantity
                                                " placeholder="0" min="0"
                                                        class="w-14 border text-sm font-light text-center" />
                                        </td>
                                        <td class="px-4 text-sm text-right">
                                                {{ calcSubtotal(item) }} €
                                        </td>
                                </tr>
                                <tr class="h-16">
                                        <td></td>
                                        <td></td>
                                        <td></td>
                                        <td class="px-4 text-m font-semibold text-cyan-700 text-right small-caps">
                                                Total
                                        </td>
                                        <td class="px-4 text-sm small-caps font-semibold text-right">
                                                {{ sumTotal }} €
                                        </td>
                                </tr>
                        </tbody>
                </table>
        </div>
        <footer class="text-center text-xs font-thin mt-20 text-cyan-700">
                «Website ex machina. XII-MMXXII.»
        </footer>
</template>

<style scoped>
.small-caps {
        font-variant-caps: all-small-caps;
}

.secondary-bg-grad {
        background-image: linear-gradient(rgb(8 145 178),
                        white,
                        rgb(8 145 178));
}
</style>
