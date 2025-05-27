<template>
  <!-- Adding Background Image -->
  <v-app 
    class="bg-cover bg-center"
    style="
    background-image: url('https://m.media-amazon.com/images/I/81GBjYL1ieL._AC_UF1000,1000_QL80_.jpg'); 
    background-size: cover;
    background-position: center;
    min-height: 100vh;"
  >
    <v-app-bar
      flat
      color="#A79E9E"
      class="border rounded-pill px-4 mt-2"
      height="64"
    >
      <!-- Logo + App Name -->
      <v-toolbar-title class="d-flex align-center">
        <v-icon class="mb-1 mr-2" color="#D50000">mdi-sofa-single</v-icon>
        <span class="font-weight-bold">kAIyu</span>
      </v-toolbar-title>


      <v-spacer />

      <!-- Center Tabs -->
      <div class="d-flex justify-center flex-grow-1">
        <v-tabs
          center-active
          color="black"
          slider-color="#D50000"
        >
          <v-tab value="home">
            <v-icon class="mr-2">mdi-home</v-icon>
            HOME
          </v-tab>
          <v-tab value="generate">
            <v-icon class="mr-2">mdi-creation</v-icon>
            GENERATE
          </v-tab>
          <v-tab value="gallery">
            <v-icon class="mr-2">mdi-view-gallery</v-icon>
            GALLERY
          </v-tab>
          <v-tab value="about">
            <v-icon class="mr-2">mdi-information</v-icon>
            ABOUT
          </v-tab>
        </v-tabs>
      </div>

      <v-spacer />

      <!-- Right Section: Sign Up + Avatar -->
      <v-btn variant="text" class="text-red font-weight-bold mr-2">
        Sign Up
      </v-btn>

      <!-- Avatar dropdown -->
      <v-menu offset-y>
        <template #activator="{ props }">
          <v-btn icon v-bind="props" class="mr-2" color="white">
            <v-icon>mdi-account</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item @click="openSettings" class="px-5">
            <v-list-item-title>
              <v-icon class="mr-6">mdi-cog</v-icon>
              <v-btn>Settings</v-btn>
            </v-list-item-title>
          </v-list-item>
          <v-list-item @click="logout" class="px-5">
            <v-list-item-title>
              <v-icon class="mr-6">mdi-logout</v-icon>
              <v-btn>Logout</v-btn>
            </v-list-item-title>
          </v-list-item>
          <v-list-item @click="toggleTheme">
            <v-list-item-title>
              <v-icon class="mr-6">mdi-theme-light-dark</v-icon>
              <v-btn>Toggle Theme</v-btn>
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>   
    </v-app-bar>

    <v-container class="pa-10 mt-5">
      <v-row>
        <v-col class="mt-10" cols="12">
          <div class="text-center font-weight-bold text-h5 text-black">
            DECORATION GENERATOR
          </div>
          <div class="text-center text-body-1 mt-5 text-black">
            Where AI Meets Design: Transforming Spaces Without the Stress
          </div>
        </v-col>
      </v-row>
    </v-container>
    
    <v-container>
      <v-row>
        <!-- Upload Room -->
        <v-col cols="12" md="6" sm="4">
          <v-card class="pa-4" elevation="4" rounded>
            <v-card-item>
              <v-card-title>
                Upload Existing Room
              </v-card-title>
            </v-card-item>
            <v-file-input label="Upload Photo" prepend-icon="mdi-upload" class="mt-2"></v-file-input>
            <v-card-actions>
              <v-btn variant="outlined" color="#D50000" prepend-icon="mdi-camera">Snapshot</v-btn>
              <v-btn variant="outlined" color="#D50000" prepend-icon="mdi-upload">Upload</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
        <!-- Room Type -->
        <v-col cols="12" md="6" sm="4">
          <v-card class="pa-4" elevation="4" rounded>
            <v-card-item>
              <v-card-title>Room Type</v-card-title>
              <v-select :items="['Bedroom', 'Living Room', 'Kitchen']" label="Select One" class="mt-2"></v-select>
            </v-card-item>
            <v-card-item>
              <!-- Design Style -->
              <v-card-title>Design Style</v-card-title>
              <v-actions>
                <v-responsive class="overflow-y-auto" max-height="200">
                  <v-chip-group
                    class="mt-2"
                    selected-class="text-primary"
                    column
                    >
                    <v-chip
                    v-for="tag in tags"
                    :key="tag"
                    :text="tag"
                    ></v-chip>
                  </v-chip-group>
                </v-responsive>
                <v-btn block="Block Button" class="mt-4" color="#D50000" prepend-icon="mdi-creation">Generate Image</v-btn>
              </v-actions>
            </v-card-item>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <v-container>
      <v-row>
      <v-col cols="12">
        <v-sheet class="pa-4" elevation="5" rounded>
          <div class="text-body-1 font-weight-bold mb-2">Design | Gallery</div>
          <v-carousel show-arrows="hover" hide-delimiter-background="">
            <v-carousel-item
              v-for="(item, i) in items"
              :key="i"
              :src="item.src"
              cover
            ></v-carousel-item>
          </v-carousel>
        </v-sheet>
      </v-col>
    </v-row>
    </v-container>

  </v-app>
  

</template>

<script setup>

  const tags = [
    'Modern',
    'Minimalism',
    'Classic',
    'Ikea',
    'Rustic',
    'Industrial',
    'Traditional',
    'Bohemian',
    'Modern Farmhouse',
  ]

  const items = [
    {
      src: 'https://homefirstindia.com/app/uploads/2020/12/Living-Room.jpg'
    },
    {
      src: 'https://d28pk2nlhhgcne.cloudfront.net/assets/app/uploads/sites/3/2021/11/living-room-decoration-720x533.jpg'
    },
    {
      src: 'https://www.kunstloft.com/magazine/wp-content/uploads/2024/01/home-decoration-with-a-small-budget-2000x1128.webp'
    }
  ]
</script>
