<template>
    <div class="table-responsive">
        <table class="table table-striped table-sm">
            <thead>
                <tr>
                    <th>Link</th>
                    <th>Users</th>
                    <th>Revenue</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="link in links" :key="link.id">
                    <td>{{ checkoutUrl(link.code) }}</td>
                    <td>{{ link.account }}</td>
                    <td>{{ link.revenue }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script lang="ts">
import { ref } from '@vue/reactivity'
import { Link } from '@/models/link'
import { onMounted } from '@vue/runtime-core';
import axios from "axios";

export default {
    name: "Stats",
    setup() {
        const links = ref<Link>([]);

        onMounted( async () => {
            const {data} = await axios.get('stats');

            links.value = data;
        });

        const checkoutUrl = (code: string) => `https://ecommerce.adrianstudio.es/${code}`;

        return {
            links,
            checkoutUrl
        }
    }
}
</script>