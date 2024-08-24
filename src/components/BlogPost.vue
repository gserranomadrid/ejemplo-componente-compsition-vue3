<script setup>
//defineProps(['title', 'id', 'body', 'colorText'])
defineProps ({
    id: Number,
    title: String,
    body:{
        type: String,
        default: "Sin descripción",
    },
    cambiarFavorito: Function,
});

//const emit = defineEmits(['cambiarFavoritos'])
//emit ('cambiarFavoritos', title)
</script>

<template>
    <div class="card">
        <div class="card-body">
            <!-- <h5 class="card-title" :class="`text-${colorText}`">{{ id }}-{{title}}</h5> -->
            <h5 class="card-title">{{ id }}-{{title}}</h5>
            <p>{{ body}}</p>
            <button class="btn btn-outline-primary" @click="cambiarFavorito(title)"> Favorito</button>
        </div>
    </div>
</template>