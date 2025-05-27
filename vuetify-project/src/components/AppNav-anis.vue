<template>
    <v-container style="position: fixed; z-index: 1000; top: 16px; left: 16px; right: 16px;">
        <v-toolbar elevation="4" style="border-radius: 33px;">

            <template v-slot:prepend>
                <v-btn @click="toggleTheme" icon="mdi-lightbulb" variant="plain" :ripple="false"></v-btn>
                <v-btn to="/" variant="plain" :ripple="false">
                    <img src="@/assets/logo.png" alt="Logo" height="24" class="mr-2">
                    k-AI-yu
                </v-btn>
            </template>

                <v-btn variant="plain" to="/generate" :ripple="false">Generate</v-btn>
                <v-btn variant="plain" to="/about" :ripple="false" class="ml-4">About</v-btn>
                <v-btn variant="plain" to="/gallery" :ripple="false" class="ml-4">Gallery</v-btn>

            <template v-slot:append>
                <v-btn variant="text" color="deep-purple-darken-2" size="auto" density="compact"
                    style="margin-left: 12px;" :ripple="false" @click="dialog = !dialog">sign-up</v-btn>
                <v-btn icon="mdi-account" class="ml-2"></v-btn>
                <v-btn icon="mdi-wrench" class="ml-2"></v-btn>
            </template>
        </v-toolbar>
    </v-container>

</template>

<script setup>
import { useTheme } from 'vuetify';
import { ref } from 'vue';
 
const theme = useTheme();
const dialog = ref(false);

function toggleTheme() {
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark';
}
</script>

<style></style>