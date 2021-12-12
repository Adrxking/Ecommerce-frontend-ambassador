<template>
    <Nav />

<main>

  <Header v-if="showHeader" />

  <div class="album py-5 bg-light">
    <div class="container">
      <router-view />
    </div>
  </div>

</main>
</template>

<script>
import Nav from '@/components/Nav.vue'
import Header from '@/components/Header.vue'
import {computed, onMounted} from "vue"
import {useStore} from "vuex"
import {useRoute} from "vue-router"
import axios from "axios"

export default {
    name: "Layout",
    components: { Header, Nav },
    setup() {
        const store = useStore();
        const route = useRoute();

        // Esconder el balance de dinero si no estamos en los siguientes enlaces
        const showHeader = computed(() => route.path === '/' || route.path === '/backend');

        onMounted(async () => {
            try {
                const {data} = await axios.get('user');
                
                await store.dispatch('setUser', data);
            } catch (e) {
                await store.dispatch('setUser', null);
            }

        });

        return {
          showHeader,
        }
    }
}
</script>