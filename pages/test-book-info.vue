<template>
    <BookInfo v-bind:index="1" v-bind:linkable="true" v-bind:book="book0" />
    <BookInfo v-bind:linkable="false" v-bind:book="book1" />
</template>

<script setup lang="ts">
import type { Book } from "@/interfaces"

const book0: Book = { title: "Alpha title", author: "Alpha author", publisher: "Alpha publisher", published: new Date(), price: 100 }
const book1: Book = { title: "Bravo title", author: "Bravo author", publisher: "Bravo publisher", published: new Date(), price: 200 }

</script>