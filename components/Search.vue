<template>
    <v-text-field label="キーワード" v-model="keyword"></v-text-field>
    <v-btn v-on:click="onClick">検索</v-btn>
    <BookInfo v-for="(book, index) of books" v-bind:linkable="true" v-bind:book="book" v-bind:index="index + 1"
        v-bind:key="book.id"></BookInfo>
</template>

<script setup lang="ts">
import type { Book } from "@/interfaces"

const keyword = ref("")
const books: Ref<[Book]> = ref()

const onClick = async () => {
    books.value = []
    const { data } = await useFetch("https://www.googleapis.com/books/v1/volumes", { query: { q: keyword.value } })
    for (const item of data.value.items) {
        const authors = item.volumeInfo.authors
        const price = item.saleInfo.listPrice
        const img = item.volumeInfo.imageLinks
        books.value.push({
            id: item.id,
            title: item.volumeInfo.title,
            author: authors ? authors.join(",") : "",
            price: price ? price.amount : "-",
            publisher: item.volumeInfo.publisher,
            published: item.volumeInfo.publishedDate,
            image: img ? img.smallThumbnail : "",
        })
    }
}

</script>