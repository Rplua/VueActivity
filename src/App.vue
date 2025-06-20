<template>
  <div class="bg-gradient bg-dark text-light min-vh-100 py-5">
    <div class="container">
      <div class="text-center mb-5">
        <h1 class="display-5 fw-bold text-info">📇 Contact Manager</h1>
        <p class="lead text-secondary">Organiza tus contactos y genera números de la suerte</p>
      </div>
      <div class="card bg-secondary bg-opacity-25 shadow-sm mb-5">
        <div class="card-body row gy-3">
          <div class="col-md-6">
            <label class="form-label text-white-50 fw-semibold">Contact Owner Name</label>
            <input
              v-model="contactOwner"
              type="text"
              class="form-control bg-light text-dark border-0 shadow-sm"
              placeholder="e.g. Randy"
            />
          </div>
          <div class="col-md-6">
            <label class="form-label text-white-50 fw-semibold">Max Lucky Number</label>
            <input
              v-model="maxNumber"
              type="number"
              class="form-control bg-light text-dark border-0 shadow-sm"
              placeholder="e.g. 100"
            />
          </div>
        </div>
      </div>
      <div class="mb-5">
        <AddContact :onAddContact="onAddContact" />
      </div>
      <div>
        <h3 class="text-center text-info mb-4">👥 Lista de Contactos</h3>
        <div class="row g-4">
          <div
            class="col-12 col-sm-6 col-lg-4"
            v-for="contact in contacts"
            :key="contact.name"
          >
            <Contact
              :name="contact.name"
              :phone="contact.phone"
              :ownerName="contact.ownerName"
              :email="contact.email"
              :isFavorite="contact.isFavorite"
              @update-favorite="contact.isFavorite = onUpdateFavorite($event)"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Contact from './components/Contact.vue'
import { ref, provide } from 'vue'
import AddContact from './components/AddContact.vue'

export default {
  components: {
    Contact,
    AddContact,
  },
  setup() {
    const contactOwner = ref("Randy")
    const maxNumber = ref(10230)
    provide("maxLuckyNumber", maxNumber)

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
