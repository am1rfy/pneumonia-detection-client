<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-space />

        <div class="flex items-center justify-center">
          Распознавание пневмонии v1.0.0
          <q-avatar icon="info" size="xl">
            <q-tooltip
              transition-show="scale"
              transition-hide="scale"
              anchor="bottom start"
              self="top start"
            >
              <span style="font-size: 14px">
                Данный программный продукт представляет собой решение для
                распознавания пневмонии по рентгеновскому снимку пациента.<br />
                Анализируя медицинские изображения, система быстро предоставляет
                оценку, помогающую врачам в диагностике и принятии решений.<br />
                В основе программного продукта лежит модель машинного обучения,
                построенная на базе сверточной нейронной сети (CNN).<br />
                Модель демонстрирует высокую точность, достигая примерно 92,6%.
              </span>
            </q-tooltip>
          </q-avatar>
        </div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

defineOptions({
  name: "MainLayout",
});

const linksList = [
  {
    title: "Docs",
    caption: "quasar.dev",
    icon: "school",
    link: "https://quasar.dev",
  },
  {
    title: "Github",
    caption: "github.com/quasarframework",
    icon: "code",
    link: "https://github.com/quasarframework",
  },
  {
    title: "Discord Chat Channel",
    caption: "chat.quasar.dev",
    icon: "chat",
    link: "https://chat.quasar.dev",
  },
  {
    title: "Forum",
    caption: "forum.quasar.dev",
    icon: "record_voice_over",
    link: "https://forum.quasar.dev",
  },
  {
    title: "Twitter",
    caption: "@quasarframework",
    icon: "rss_feed",
    link: "https://twitter.quasar.dev",
  },
  {
    title: "Facebook",
    caption: "@QuasarFramework",
    icon: "public",
    link: "https://facebook.quasar.dev",
  },
  {
    title: "Quasar Awesome",
    caption: "Community Quasar projects",
    icon: "favorite",
    link: "https://awesome.quasar.dev",
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>
