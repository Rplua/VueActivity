<template>
  <div class="bg-black text pt-3" :style="{ height: '100hv' }">
    <div class="container">
      <div class="row text-white p-2 mb-2">
        <div class="col-6">
          Contact Owner Name: <input v-model="contactOwner">
        </div>
        <div class="col-6 text-end">
          Max Lucky Number : <input v-model="maxNumber">
        </div>
      </div>
      <div>
        <div class="text-white float-end">

        </div>
      </div>
      <br>
      <AddContact @add-contact="onAddContact"></AddContact>
      <div class="row">
        <div class="col-12" v-for="contact in contacts" :key="contact.name">
          <Contact :name="contact.name" :phone="contact.phone" :ownerName="contact.ownerName" :email="contact.email"
            :isFavorite="contact.isFavorite" @update-favorite="contact.isFavorite = onUpdateFavorite($event)"
            :maxLuckyNumber="maxNumber" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Contact from './components/Contact.vue'
import { ref } from 'vue'
import AddContact from './components/AddContact.vue'


export default {
  components: {
    Contact,
    AddContact,
  },
  setup() {
    const contactOwner = ref("Randy")
    const maxNumber = ref(100);
    const contacts = ref([
      {
        name: 'Alice Johnson',
        phone: '123-456-7890',
        email: 'alice@example.com',
        ownerName: contactOwner.value,
        isFavorite: true
      },
      {
        name: 'Bob Smith',
        phone: '555-123-4567',
        email: 'bob@example.com',
        ownerName: contactOwner.value,
        isFavorite: true
      },
      {
        name: 'Charlie Davis',
        phone: '987-654-3210',
        email: 'charlie@example.com',
        ownerName: contactOwner.value,
        isFavorite: false
      },
      {
        name: 'Dana Lee',
        phone: '444-555-6666',
        email: 'dana@example.com',
        ownerName: contactOwner.value,
        isFavorite: false
      }
    ])

    const onUpdateFavorite = (isFavoriteFromChild) => {
      return !isFavoriteFromChild
    }

    const onAddContact = (newContact) => {
      newContact.ownerName = contactOwner.value
      newContact.isFavorite = false
      contacts.value.push(newContact)
    }

    return {
      contactOwner,
      contacts,
      onUpdateFavorite,
      onAddContact,
      maxNumber
    }
  }
}
</script>