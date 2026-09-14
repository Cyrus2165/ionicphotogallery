<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Photo Gallery</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-grid>
        <ion-row>
          <ion-col
            size="6"
            v-for="(photo, index) in photos"
            :key="index"
          >
            <ion-card class="photo-card">
              <ion-img :src="photo"></ion-img>

              <ion-button
                expand="block"
                color="danger"
                @click="deletePhoto(index)"
              >
                Delete
              </ion-button>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>

      <ion-text
        v-if="photos.length === 0"
        class="empty-gallery"
      >
        <p>No photos available.</p>
      </ion-text>
    </ion-card-content>
  </ion-card>
</template>

<script setup>
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonGrid,
  IonRow,
  IonCol,
  IonImg,
  IonButton,
  IonText
} from '@ionic/vue'

const props = defineProps({
  photos: {
    type: Array,
    default: () => []
  }
})

const emit = defineEmits(['delete-photo'])

const deletePhoto = (index) => {
  emit('delete-photo', index)
}
</script>

<style scoped>
.photo-card {
  margin: 8px;
}

ion-img {
  height: 200px;
  object-fit: cover;
}

.empty-gallery {
  display: block;
  text-align: center;
  margin: 20px;
}
</style>
