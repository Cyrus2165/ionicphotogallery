<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Camera</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-text>
        <h2>Take a Photo</h2>
        <p>Capture a photo using your camera.</p>
      </ion-text>

      <ion-button expand="block" @click="takePhoto">
        <ion-icon
          :icon="cameraOutline"
          slot="start"
        ></ion-icon>
        Take Photo
      </ion-button>
    </ion-card-content>
  </ion-card>
</template>

<script setup>
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonText,
  IonButton,
  IonIcon
} from '@ionic/vue'

import { cameraOutline } from 'ionicons/icons'

import {
  Camera,
  CameraResultType,
  CameraSource
} from '@capacitor/camera'

const emit = defineEmits(['photo-taken'])

const takePhoto = async () => {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Camera
    })

    if (image.dataUrl) {
      emit('photo-taken', image.dataUrl)
    }
  } catch (error) {
    console.error('Camera error:', error)
  }
}
</script>
