<template>
    <v-navigation-drawer>
        <v-list>
            <v-list-item v-for="item in inLinks" v-bind:key="item.key" v-bind:title="item.title"
                v-bind:to="item.to"></v-list-item>
            <v-list-item v-for="item in extLinks" v-bind:key="item.key" v-bind:title="item.title" v-bind:href="item.href"
                target="_blank"></v-list-item>
        </v-list>
    </v-navigation-drawer>
</template>

<script setup lang="ts">
class InternalLink {
    key: string
    title: string
    to: string
    constructor(key: string, title: string, to: string) {
        this.key = key
        this.title = title
        this.to = to
    }
}

class ExternalLink {
    key: string
    title: string
    href: string
    constructor(key: string, title: string, href: string) {
        this.key = key
        this.title = title
        this.href = href
    }
}

const inLinks = ref([
    new InternalLink("home", "Home", "/home"),
    new InternalLink("search", "Search", "/search"),
])
const extLinks = ref([
    new ExternalLink("author", "Author", "https://wings.msn.to"),
    new ExternalLink("publisher", "Publisher", "https://www.sbcr.jp")
])
</script>