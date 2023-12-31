<template>
    <v-alert v-show="alert" title="Reading Recorder" text="読書情報の登録/更新に成功しました" type="success"></v-alert>
    <BookInfo v-bind:book="book" v-bind:linkable="false" />
    <v-form v-on:submit.prevent="onSubmit">
        <v-row>
            <v-col cols="4">
                <v-date-picker v-model="form.read"></v-date-picker>
            </v-col>
            <v-col cols="8">
                <v-textarea label="感想" v-model="form.memo"></v-textarea>
            </v-col>
        </v-row>
        <v-btn type="submit">登録</v-btn>
    </v-form>
</template>

<script setup lang="ts">
import type { Book } from "@/interfaces"

const form = reactive({
    read: new Date(),
    memo: "",
})

const alert = ref(false)

const selectedBookCookie = useCookie<Book>("selectedBook")
const book = selectedBookCookie.value

const onSubmit = () => {
    console.log("onSubmit")
    alert.value = true
    setTimeout(() => {
        alert.value = false
        navigateTo("home")
    }, 3000)
}

</script>