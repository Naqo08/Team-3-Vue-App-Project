<template>
    <v-container style="position: fixed; z-index: 1000; top: 16px; left: 0px; right: 0px;">
        <v-toolbar elevation="4" style="border-radius: 33px;">

            <!-- Logo + App Name  -->
            <template v-slot:prepend>
                <!-- <v-btn prepend-icon="mdi-sofa" to="landing" variant="plain" color="black" :ripple="false">
                    <img src="@/assets/kAIyu.png" alt="Logo" height="30" class="mr-2">
                    k-AI-yu
                </v-btn> -->
                <v-btn to="landing" variant="plain" color="black" :ripple="false">
                  <img src="@/assets/chair-icon.png" alt="chair-icon" class="custom-icon mr-2">
                  k-AI-yu
                </v-btn>
            </template>

            <!-- Center Tabs -->
                <!-- <v-btn prepend-icon="mdi-home" variant="plain" to="/generate" :ripple="false" class="ml-2">
                    Home
                </v-btn> -->
                <v-btn prepend-icon="mdi-creation" variant="plain" to="/generate" :ripple="false" class="ml-4">
                    Generate
                </v-btn>
                <v-btn prepend-icon="mdi-information" variant="plain" to="/about" :ripple="false" class="ml-4">
                    About
                </v-btn>
                <v-btn prepend-icon="mdi-view-gallery" variant="plain" to="/gallery" :ripple="false" class="ml-4">
                    Gallery
                </v-btn>

            <!-- Right Section: Sign Up + Avatar -->
            <template v-slot:append>
                <v-btn variant="text" color="black" size="auto" density="compact"
                    style="margin-left: 12px;" :ripple="false" @click="dialog = !dialog">sign-up</v-btn>

            <!-- Avatar dropdown -->
            <v-menu offset-y>
              <template #activator="{ props }">
                <v-btn icon v-bind="props" class="ml-2" color="black">
                  <v-icon>mdi-account</v-icon>
                </v-btn>
              </template>
              <v-list>
                <v-list-item @click="openSettings">
                  <v-list-item-title>
                    <v-btn prepend-icon="mdi-cog">Settings</v-btn>
                  </v-list-item-title>
                </v-list-item>
                <v-list-item @click="logout">
                  <v-list-item-title>
                    <v-btn prepend-icon="mdi-logout">Logout</v-btn>
                  </v-list-item-title>
                </v-list-item>
                <v-list-item @click="toggleTheme">
                  <v-list-item-title>
                    <v-btn prepend-icon="mdi-theme-light-dark">Toggle Theme</v-btn>
                  </v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
            </template>
        </v-toolbar>
    </v-container>
</template>

<script setup>
import { useTheme } from 'vuetify';
import { ref } from 'vue';
 
const theme = useTheme();
const dialog = ref(false);

theme.global.name.value = 'light';

function toggleTheme() {
   // theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark';
   theme.global.name.value = 'light';
}
</script>

<style scoped>
.custom-icon {
  height: 28px;
  width: 28px;
  border-radius: 50%;
  filter: grayscale(100%);
  transition: all 0.3s ease;
  object-fit: cover;
  vertical-align: middle;
}

.v-btn:hover .custom-icon {
  filter: grayscale(0%);
  transform: scale(1.1);
}
</style>