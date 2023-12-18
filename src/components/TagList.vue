<template>
  <div class="tag-list" ref="tagListRef" :style="getContainerStyles">
    <v-row v-if="visibleTags.length > 0 ">
      <v-col
          v-for="(tag, index) in visibleTags"
          :key="index"
          :style="getItemStyles(index)"
        >
        <span>{{ tag.text }}</span>
        <v-icon v-if="tag.icon" >{{ tag.icon }}</v-icon>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "TagList",
  data() {
    return {
      tagList: ''
    }
  },
  props: {
    tags: {
      type: Array,
      default: () => [],
    },
    alignment: {
      type: String,
      default: 'left',
    },
  },

  computed: {
    visibleTags() {
      const containerWidth = this.tagList.clientWidth;
      let totalWidth = 0;
      const visibleTags = [];

      for (const tag of this.tags) {
        const tagWidth = this.getTagWidth(tag);
        totalWidth += tagWidth;

        if (totalWidth <= containerWidth) {
          visibleTags.push(tag);
        } else {
          break;
        }
      }

      return visibleTags;
    },
    getContainerStyles() {
      return {
        'text-align': this.alignment,
      };
    },
  },

  methods: {
    getTagWidth(tag) {
      const iconWidth = tag.icon ? 24 : 0; // ширина иконки
      const tagTextWidth = tag.text.length * 8; // ширина текста
      return iconWidth + tagTextWidth + 16;
    },
    getItemStyles(index) {
      if (this.alignment === 'justify') {
        return index === 0 ? {} : { 'margin-left': 'auto' };
      }
      return {};
    },
  },

  mounted() {
    // Получение доступа к элементу по его ref
    this.tagList = this.$refs.tagListRef;

    // console.log(this.tagList.clientWidth );
  }
}
</script>

<style lang="scss" scoped>
.tag-list {
  display: flex;
  flex-wrap: nowrap;
  overflow: hidden;
  border: 2px solid #000000;
}

.tag-item {
  display: flex;
  align-items: center;
  padding: 4px 8px;
  border: 2px solid red;
}

.tag-item--separator::after {
  content: '';
  display: inline-block;
  width: 1px;
  height: 10px; /* Adjust separator height as needed */
  margin: 0 8px; /* Adjust separator margin as needed */
  background-color: #000; /* Adjust separator color as needed */
  border: 2px solid yellow;
}
</style>