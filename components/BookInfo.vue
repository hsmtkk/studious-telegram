<template>
    <v-container v-bind:class="{ 'linkable': props.linkable }" v-on:click="clicked">
        <v-row>
            <v-col cols="3">
                <v-img v-bind:lazy-src="props.book.image" v-bind:src="props.book.image"></v-img>
            </v-col>
            <v-col cols="9">
                <v-list>
                    <v-list-item v-if="props.index" v-bind:title="index"></v-list-item>
                    <v-list-item v-bind:title="titlePrice"></v-list-item>
                    <v-list-item v-bind:title="author"></v-list-item>
                    <v-list-item v-bind:title="publisher"></v-list-item>
                    <v-list-item v-bind:title="published"></v-list-item>
                </v-list>
            </v-col>
        </v-row>
    </v-container>
</template>

<script setup lang="ts">
import type { Book } from "@/interfaces"

interface Props {
    index?: number
    linkable: boolean
    book: Book
}

const props = defineProps<Props>()

const index = computed(() => {
    return `${props.index}.`
})

const titlePrice = computed(() => {
    return `${props.book.title} (${props.book.price})円`
})

const author = computed(() => {
    return `${props.book.author} /著`
})

const publisher = computed(() => {
    return `${props.book.publisher} /刊`
})

const published = computed(() => {
    return `${props.book.published.toLocaleString()} /発売`
})

const clicked = () => {
    console.log("clicked")
    const selectedBookCookie = useCookie<Book | null>("selectedBook")
    selectedBookCookie.value = props.book
    navigateTo("form")
}

</script>

<style scoped>
.linkable:hover {
    cursor: pointer;
    background-color: #ff9;
}
</style>