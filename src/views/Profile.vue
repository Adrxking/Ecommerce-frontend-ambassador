<template>
    <h3>Account Information</h3>
        <form @submit.prevent="infoSubmit">
            <div class="mb-3">
                <label>First Name</label>
                <input name="first_name" class="form-control" v-model="infoData.first_name" />
            </div>
            <div class="mb-3">
                <label>Last Name</label>
                <input name="last_name" class="form-control" v-model="infoData.last_name" />
            </div>
            <div class="mb-3">
                <label>Email</label>
                <input name="email" class="form-control" type="email" v-model="infoData.email" />
            </div>
            <button class="btn btn-outline-secondary">Submit</button>
        </form>

        <h3 class="mt-4">Change password</h3>
        <form @submit.prevent="passwordSubmit">
            <div class="mb-3">
                <label>Password</label>
                <input name="paswword" class="form-control" v-model="passwordData.password" />
            </div>
            <div class="mb-3">
                <label>Password Confirm</label>
                <input name="paswword_confirm" class="form-control" v-model="passwordData.password_confirm" />
            </div>
            <button class="btn btn-outline-secondary">Submit</button>
        </form>
</template>

<script>
import { computed, reactive } from '@vue/reactivity'
import { watch } from '@vue/runtime-core';
import { useStore } from 'vuex';
import axios from 'axios'

export default {
    name: "Profile",
    setup() {
        const store = useStore();
        const user = computed(() => store.state.user);
        const infoData = reactive({
            first_name: user.value.first_name,
            last_name: user.value.last_name,
            email: user.value.email,
        });

        const passwordData = reactive({
            password: '',
            password_confirm: '',
        });

        watch(user, () => {
            infoData.first_name = user.value.first_name;
            infoData.last_name = user.value.last_name;
            infoData.email = user.value.email;
        });

        const infoSubmit = async () => {
            const {data} = await axios.put('users/info', infoData);
            await store.dispatch('setUser', data);
        }

        const passwordSubmit = async () => {
            await axios.put('users/password', passwordData);
        }

        return {
            infoData,
            passwordData,
            infoSubmit,
            passwordSubmit
        }
    }
}
</script>