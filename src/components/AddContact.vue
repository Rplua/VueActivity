<template>
    <div class="container border rounder p-2">
        <div class="text-center text-white">Add New Contact</div>
        <form @submit.prevent="addContact">
            <div class="row">
                <div class="col-4">
                    <input type="text" class="form-control" v-model="contact.name" placeholder="name">
                </div>
                <div class="col-4">
                    <input type="text" class="form-control" v-model="contact.email" placeholder="email">
                </div>
                <div class="col-4">
                    <input type="text" class="form-control" v-model.number="contact.phone" placeholder="phone">
                </div>
                <div class="col-6 offset-3 p-2">
                    <button type="submit" class="btn btn-secondary w-100">Add Contact</button>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
import { reactive } from 'vue'

export default {
    name: 'AddContact',
    emits: ['add-contact'],
    setup(_, { emit }) {
        const contact = reactive({
            name: "",
            phone: "",
            email: ""
        })

        const addContact = () => {
            emit("add-contact", { ...contact })
            contact.name = ""
            contact.phone = ""
            contact.email = ""
        }

        return {
            contact,
            addContact
        }
    }
}
</script>