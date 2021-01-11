<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Plans</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Plans</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id="planarr">
        <ion-list v-for="(item) in items" :key="item.name">
          <ion-item>
            <ion-label @click="presentActionSheet">
              <h2>{{item.name}}</h2>
              <h3>{{amountFormat(item.value)}}</h3>
              <p>{{item.date}}</p>
            </ion-label>
          </ion-item>
        </ion-list>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {  actionSheetController ,IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import {  close, trash, share } from 'ionicons/icons';


export default  {
  name: 'Tab2',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  el:'#planarr',

  data() {
    return {
      items: [
        {name: 'Pay to bro', value: -100000, date:"2023-12-15"},
        {name: 'Take', value: 330000, date:"2024-12-15"},
        {name: 'Borrow', value: 100, date:"2025-12-15"}
      ]
    }
  },

  methods: {
    amountFormat: function (value: number) {
      return new Intl.NumberFormat().format(value);
    },
    async presentActionSheet() {
      const actionSheet = await actionSheetController
          .create({
            header: 'Albums',
            cssClass: 'my-custom-class',
            buttons: [
              {
                text: 'Delete',
                role: 'destructive',
                icon: trash,
                handler: () => {
                  console.log('Delete clicked')
                },
              },
              {
                text: 'Change',
                icon: share,
                handler: () => {
                  console.log('Change clicked')
                },
              },
              {
                text: 'Cancel',
                icon: close,
                role: 'cancel',
                handler: () => {
                  console.log('Cancel clicked')
                },
              },
            ],
          });
      return actionSheet.present();
    }
  }
}
</script>