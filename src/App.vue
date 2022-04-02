<template>
  <v-app>
    <TagString :alignment="alignment" :tags="tags" />
  </v-app>
</template>

<script>
import TagString from "@/components/TagString";

export default {
  components: {
    TagString,
  },
  data: () => ({
    alignment: "start",
    tags: [
      { icon: "mdi-star-outline", text: "*****" },
      {},
      {
        icon: "mdi-star-outline",
        text: "Координаты: 55°45′20.9916″N, 37°37′3.6228″E",
      },
      { icon: null, text: "Фриландские ворота" },
      { icon: "mdi-star-outline", text: "1.2 км от вас" },
      { icon: "mdi-star-four-points-outline", text: "Рекомендуем" },
      { text: "Эконом" },
    ],
  }),
};
</script>
