<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

      </q-toolbar>
      <div class="q-px-lg q-pt-lg-xl q-mb-md">
        <div class="text-h3">My daily to do list</div>
        <div class="text-subtitle1">{{todaysDate }}</div>
        <div class="text-subtitle1">  {{hebDate}}</div>
        <div class="text-subtitle1">פרשת השבוע: {{parasha}}</div>
      </div>
      <q-img
        class="header-image absolute-top"
        src="https://cdn.pixabay.com/photo/2013/11/28/10/36/road-220058_960_720.jpg"
      />
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="256"
      :breakpoint="600"
    >
      <q-scroll-area style="height: calc(100% - 256px); margin-top: 256px; border-right: 1px solid #ddd">
        <q-list padding>
          <q-item
            to="/"
            exact
            clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section>
              Missions to do!
            </q-item-section>
          </q-item>

          <q-item to="/help"
                  exact
                  clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section>
              Help
            </q-item-section>
          </q-item>

        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top" src="https://cdn.pixabay.com/photo/2013/11/28/10/36/road-220058_960_720.jpg" style="height: 256px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://cdn.quasar.dev/img/boy-avatar.png" alt="Img">
          </q-avatar>

          <div class="text-weight-bold">Yair Machta</div>
          <div>@machtayair</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view/>
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>


<script>
import {date} from 'quasar'
import EssentialLink from 'components/EssentialLink.vue'
import Hebcal from "hebcal";

const linksData = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
];

export default {
  name: 'MainLayout',
  components: {
    EssentialLink
  },

  data() {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData,
    }
  },

  computed: {
    todaysDate() {
      const timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM');
    },
    hebDate() {
      return new Hebcal.HDate()
    },
    parasha(){
      let parash = new Hebcal.HDate().getSedra('h')
      return parash.toString();
    }
  }

}
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.2;
  filter: grayscale(100%);
}
</style>
