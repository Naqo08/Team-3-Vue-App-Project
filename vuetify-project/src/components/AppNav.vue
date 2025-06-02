<template>
  <v-container style="position: fixed; z-index: 1000; top: 16px; left: 0px; right: 0px;">
    <v-toolbar color="#4A2511" elevation="4" height="50" style="border-radius: 33px;">

      <!-- Logo + App Name  -->
      <template v-slot:prepend>
        <v-btn color="white" :ripple="false" to="landing" variant="plain">
          <!-- <img alt="chair-icon" class="custom-icon mr-2" src="@/assets/chair-icon.png"> -->
          <img alt="chair-icon" class="custom-icon mr-2" src="https://raw.githubusercontent.com/Naqo08/Team-3-Vue-App-Project/din-branch/images-logo/chair-icon.png">
          k-AI-yu
        </v-btn>
      </template>

      <!-- Center Tabs -->
      <v-btn
        class="ml-4"
        prepend-icon="mdi-creation"
        :ripple="false"
        to="/generate"
        variant="plain"
      >
        Generate
      </v-btn>
      <v-btn
        class="ml-4"
        prepend-icon="mdi-information"
        :ripple="false"
        to="/about"
        variant="plain"
      >
        About
      </v-btn>
      <v-btn
        class="ml-4"
        prepend-icon="mdi-view-gallery"
        :ripple="false"
        to="/gallery"
        variant="plain"
      >
        Gallery
      </v-btn>

      <!-- Right Section: Sign Up + Avatar -->
      <template v-slot:append>
        <v-btn
          color="white"
          density="compact"
          :ripple="false"
          size="auto"
          style="margin-left: 12px;"
          variant="plain"
          @click="dialog = !dialog"
        >
          sign-up
        </v-btn>

        <!-- Avatar dropdown -->
        <v-menu offset-y>
          <template #activator="{ props }">
            <v-btn
              class="ml-2"
              color="white"
              icon
              v-bind="props"
              variant="plain"
            >
              <v-icon>mdi-account</v-icon>
            </v-btn>
          </template>
          <v-list class="dropdown-list">
            <v-list-item>
              <v-btn block class="dropdown-btn" prepend-icon="mdi-cog" @click="openSettings">Settings</v-btn>
            </v-list-item>
            <v-list-item>
              <v-btn block class="dropdown-btn" prepend-icon="mdi-logout" @click="logout">Logout</v-btn>
            </v-list-item>
            <v-list-item>
              <v-btn block class="dropdown-btn" prepend-icon="mdi-theme-light-dark" @click="toggleTheme">Toggle Theme</v-btn>
            </v-list-item>
          </v-list>
        </v-menu>
      </template>
    </v-toolbar>
</v-container>
</template>

<script setup lang="ts">
  import { useTheme } from 'vuetify';
  import { ref } from 'vue';

  const theme = useTheme();
  const dialog = ref(false);

  theme.global.name.value = 'light';

  function toggleTheme () {
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

.dropdown-list {
  min-width: 200px;
  padding: 4px;
}

.dropdown-btn {
  justify-content: flex-start;
  padding-left: 16px;
  text-transform: none;
  font-weight: normal;
}

.dropdown-btn ::v-deep .v-btn__prepend {
  margin-right: 12px;
  margin-left: 0;
}

.dropdown-btn:hover {
  background-color: rgba(0, 0, 0, 0.04);
}
</style>
