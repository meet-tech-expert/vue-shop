<template>
  <v-app>
    <v-app-bar dark fixed app>
      <v-row>
        <v-col cols="2"> </v-col>
        <v-col class="d-flex justify-space-around">
          <v-toolbar-title>{{ title }}</v-toolbar-title>
        </v-col>
        <v-col cols="2" class="d-flex justify-end"></v-col>
      </v-row>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer absolute app dark height="50px">
      <span
        >&copy; כל הזכויות שמורות לביוטיקייר. השימוש באתר הינו בכפוף לתקנון האתר
        דרימקס בניית אתרי מג'נטו</span
      >
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      title: "מניקור",
    };
  },
};
</script>
