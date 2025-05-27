<template>
  <AppNav />
  <v-container height="150" :fluid="true" style="padding: 0">
    <v-row>
        <v-col cols="12"></v-col>
        <v-col cols="12"></v-col>
    </v-row>
  </v-container>

  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12">
        <v-card class="text-center">
          <v-card-title>Decoration Generator</v-card-title>
          <v-card-text> Your Personal AI Decorator: Perfect Spaces at the Touch of a Button </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
  
  <v-container>
    <v-row class="fill-height">
      <!-- Left Column -->
      <v-col cols="6" class="d-flex">
        <v-card class="pa-4 flex-grow-1">
          <v-card-title>Upload Your Room Photo</v-card-title>
          <v-card-text>
            <p class="mb-4">Please upload or take a photo of your room to get started</p>
            
            <!-- Drag & Drop Zone -->
            <v-sheet
              class="upload-zone pa-16 mb-4"
              :class="{ 'dragging': isDragging }"
              rounded
              border
              @dragenter.prevent="isDragging = true"
              @dragleave.prevent="isDragging = false"
              @dragover.prevent
              @drop.prevent="handleDrop"
            >
              <div class="text-center">
                <v-icon
                  size="48"
                  color="primary"
                  icon="mdi-cloud-upload"
                  class="mb-2"
                ></v-icon>
                <div class="text-body-1 mb-2">Drag and drop your image here</div>
                <div class="text-body-2 text-medium-emphasis">or</div>
                <v-btn
                  class="mt-2"
                  color="primary"
                  variant="outlined"
                  @click="triggerUpload"
                >
                  Browse Files
                </v-btn>
              </div>
            </v-sheet>
            
            <!-- Image Preview -->
            <v-img
              v-if="imagePreview"
              :src="imagePreview"
              height="300"
              cover
              class="mb-4 rounded"
            >
              <template v-slot:placeholder>
                <v-row
                  class="fill-height ma-0"
                  align="center"
                  justify="center"
                >
                  <v-progress-circular
                    indeterminate
                    color="primary"
                  ></v-progress-circular>
                </v-row>
              </template>
            </v-img>
            
            <!-- Hidden File Input -->
            <input
              type="file"
              ref="fileInput"
              accept="image/*"
              style="display: none"
              @change="handleFileUpload"
            >
            
            <!-- Upload and Take Photo Buttons -->
            <v-row>
              <v-col cols="6">
                <v-btn
                  block
                  color="primary"
                  prepend-icon="mdi-camera"
                  @click="takePhoto"
                >
                  Take Photo
                </v-btn>
              </v-col>
              <v-col cols="6">
                <v-btn
                  block
                  color="primary"
                  prepend-icon="mdi-upload"
                  @click="triggerUpload"
                >
                  Upload Photo
                </v-btn>
                <input
                  type="file"
                  ref="fileInput"
                  accept="image/*"
                  style="display: none"
                  @change="handleFileUpload"
                >
              </v-col>
            </v-row>
            
          </v-card-text>
        </v-card>
      </v-col>
      

      <!-- Right Column -->
      <v-col cols="6" class="d-flex">
        <v-card class="pa-4 flex-grow-1">
          <v-card-title>Room Configuration</v-card-title>
          <v-card-text>
            <!-- Room Type Selection -->
            <v-select
              v-model="roomType"
              label="Room Type"
              :items="roomTypes"
              class="mb-4"
            ></v-select>

            <!-- Design Style Selection -->
            <v-radio-group
              v-model="designStyle"
              label="Design Style"
              class="mb-4"
            >
              <v-radio
                v-for="style in designStyles"
                :key="style"
                :label="style"
                :value="style"
              ></v-radio>
            </v-radio-group>

            <!-- Generate Button -->
            <v-btn
              block
              color="primary"
              size="large"
               
              @click="generateDesign"
            >
              Generate Design
            </v-btn>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Image handling
const imagePreview = ref<string | null>(null)
const fileInput = ref<HTMLInputElement | null>(null)
const isDragging = ref(false)

// Room configuration
const roomType = ref<string>('')
const designStyle = ref<string>('')

// Options for selections
const roomTypes = ['Living Room', 'Bedroom', 'Kitchen', 'Bathroom']
const designStyles = ['Modern', 'Scandinavian', 'Traditional', 'Minimalist', 'Retro']

// Methods
const triggerUpload = () => {
  fileInput.value?.click()
}

const handleFileUpload = (event: Event) => {
  const target = event.target as HTMLInputElement
  if (target.files && target.files[0]) {
    const file = target.files[0]
    imagePreview.value = URL.createObjectURL(file)
  }
}

const handleDrop = (event: DragEvent) => {
  isDragging.value = false
  const files = event.dataTransfer?.files
  if (files && files[0]) {
    const file = files[0]
    if (file.type.startsWith('image/')) {
      imagePreview.value = URL.createObjectURL(file)
    }
  }
}

const takePhoto = () => {
  // Implement camera functionality here
  console.log('Take photo clicked')
}

const generateDesign = () => {
  // Implement generation logic here
  console.log('Generating design with:', {
    roomType: roomType.value,
    designStyle: designStyle.value
  })
}
</script>

<style scoped>
.upload-zone {
  border: 2px dashed rgba(var(--v-theme-primary), 0.4) !important;
  transition: all 0.3s ease;
  cursor: pointer;
}

.upload-zone:hover {
  border-color: rgba(var(--v-theme-primary), 0.8) !important;
  background: rgba(var(--v-theme-primary), 0.05);
}

.upload-zone.dragging {
  border-color: var(--v-theme-primary) !important;
  background: rgba(var(--v-theme-primary), 0.1);
}


</style>