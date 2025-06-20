<template>
    <div class="card mb-3 shadow-sm border-primary">
        <div class="card-header bg-primary text-white d-flex justify-content-between align-items-center">
            <h5 class="mb-0">{{ name }}</h5>
            <span class="badge bg-info text-dark">{{ ownerName }}</span>
        </div>
        <div class="card-body">
            <p class="mb-2"><strong>Email:</strong> {{ email }}</p>
            <p class="mb-3"><strong>Phone:</strong> {{ phone }}</p>
            <button @click="$emit('update-favorite', isFavorite)" class="btn"
                :class="isFavorite ? 'btn-success' : 'btn-outline-secondary'">
                {{ isFavorite ? '★ Favorite' : '☆ Mark as Favorite' }}
            </button>
        </div>
        <div class="card-footer bg-light text-end">
            <LuckyNumber :maxNumber="maxLuckyNumber" />
        </div>
    </div>
</template>

<script>
import LuckyNumber from './LuckyNumber.vue'

export default {
    name: 'Contact',
    components: {
        LuckyNumber
    },
    props: {
        name: String,
        email: String,
        phone: String,
        ownerName: String,
        isFavorite: Boolean,
        maxLuckyNumber: Number
    }
}
</script>
