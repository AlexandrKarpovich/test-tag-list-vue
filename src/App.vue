<template>
  <v-app>
    <!-- Компонент на всю ширину экрана с выравниванием по левому краю -->
    <TagList :tags="tags" alignment="left"></TagList>

    <!-- Компонент на всю ширину экрана с выравниванием по ширине -->
    <TagList :tags="tags" alignment="justify"></TagList>

    <!-- Компонент на 50% ширины экрана с выравниванием по левому краю -->
    <div style="width: 50%;">
      <TagList :tags="tags" alignment="left"></TagList>
    </div>

    <!-- Компонент на 50% ширины экрана с выравниванием по ширине -->
    <div style="width: 50%;">
      <TagList :tags="tags" alignment="justify"></TagList>
    </div>

    <!-- <v-btn color="primary">Пример кнопки Vuetify</v-btn>
    <v-icon>mdi-circle-small</v-icon> -->
  </v-app>
</template>

<script>

import TagList from "@/components/TagList";
export default {
  name: 'App',
  components: {TagList},
  data() {
    return {
      tags: [
        { text: 'текст1' },
        { text: 'текст2', icon: 'mdi-circle-small' },
        // Добавьте нужные теги с текстом и иконками
      ],
    };
  },
};
</script>
