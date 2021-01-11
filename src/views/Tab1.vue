<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Accounts</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Accounts</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id="accarr">
        <ion-list v-for="(item) in items" :key="item.name">
          <ion-item @click="presentActionSheet">
            <ion-label>{{item.name}}</ion-label>
            <ion-badge v-if="item.active" slot="end">{{amountFormat(item.value)}}</ion-badge>
            <ion-badge v-else color="medium" slot="end">{{amountFormat(item.value)}}</ion-badge>
          </ion-item>
        </ion-list>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {IonPage, IonHeader, IonToolbar, IonTitle, IonContent, actionSheetController} from '@ionic/vue';
import {close, share, trash} from "ionicons/icons";

export default  {
  name: 'Tab1',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  el:'#accarr',
  data() {
    return {
      items: [
        {name: 'ank Bank', value: 100000, active: true},
        {name: 'Cash', value: 200000, active: true},
        {name: 'Convert', value: 300000, active: true},
        {name: 'Deposit in bank', value: 12000, active: false}
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