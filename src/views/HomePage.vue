<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Camera Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">

      <CameraComponents
        @photo-taken="addPhoto"
      />

      <PhotoGalleryComponent
        :photos="photos"
        @delete-photo="deletePhoto"
      />

    </ion-content>
  </ion-page>
</template>

<script setup>
import { ref } from 'vue'

import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent
} from '@ionic/vue'

import CameraComponents from '@/components/CameraComponents.vue'
import PhotoGalleryComponent from '@/components/PhotoGalleryComponent.vue'

const photos = ref([])

const addPhoto = (photo) => {
  photos.value.push(photo)
}

const deletePhoto = (index) => {
  photos.value.splice(index, 1)
}
</script>
