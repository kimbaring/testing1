<template>
  <ion-page>
    <ion-header :translucent="true" @click="sendPusher()">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
     
      
    
      <div id="container">
        <ion-button class="test" @click="sendNotif">Send Notif</ion-button>

      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton } from '@ionic/vue';
import {LocalNotifications} from '@capacitor/local-notifications';



const value = ({
  name: 'HomePage',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton
  },
  data(){
    return {
      counter: 0,
      opt: null
    };
  },  
  async mounted(){
      this.opt = {notifications:[{
            id: new Date().getTime(),
            channelId: 'test', // If you are using channels
            title: 'My Title',
            body: 'My body'
        }]}

      LocalNotifications.createChannel({
        id: 'test',
        name: 'Reminders',
        description: 'Reminders you set within App',
        importance: 4
      })
  },
  methods:{
    sendNotif(){
        setTimeout(()=>{
          LocalNotifications.schedule(this.opt);
        },5000);
    }
    
  }
});

export default value;
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
