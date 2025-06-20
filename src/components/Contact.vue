<template>
    <div class="card border-0 shadow-sm bg-gradient bg-opacity-10">
        <div class="card-header bg-primary text-white d-flex justify-content-between align-items-center">
            <h5 class="mb-0">{{ name }}</h5>
            <span class="badge bg-info text-dark">{{ ownerName }}</span>
        </div>
        <div class="card-body">
            <p class="mb-2">
                <i class="bi bi-envelope me-2 text-info"></i>
                <strong>Email:</strong> {{ email }}
            </p>
            <p class="mb-4">
                <i class="bi bi-telephone me-2 text-info"></i>
                <strong>Phone:</strong> {{ phone }}
            </p>
            <button @click="$emit('update-favorite', isFavorite)" class="btn w-100 fw-semibold"
                :class="isFavorite ? 'btn-success' : 'btn-outline-info'">
                {{ isFavorite ? '★ Favorite Contact' : '☆ Mark as Favorite' }}
            </button>
        </div>
        <div class="card-footer bg-light text-end">
            <LuckyNumber />
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
        isFavorite: Boolean
    }
}
</script>
