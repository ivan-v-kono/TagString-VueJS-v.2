<template>
  <div class="wrapper">
    <v-row class="tag-row ma-0 mt-2 pa-0 overflow-hidden" :class="aligning">
      <p
        class="tag-string ma-0 pa-0"
        v-for="(tag, index) in tags"
        :key="componentKey + index"
        :id="index"
      >
        <span class="tag" :class="visibility[index]">
          <v-icon
            class="tag-string_icon-separator"
            v-if="index > 0 && (tag.icon || tag.text)"
            color="#0808b3"
          >
            mdi-circle-small
          </v-icon>
          <v-icon class="tag-string_icon-tag"> {{ tag.icon }} </v-icon>
          {{ tag.text }}
        </span>
      </p>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "TagString",
  props: {
    alignment: String,
    tags: Array,
  },
  data: () => ({
    componentKey: 0,
    viewSize: null,
    tagLengths: [],
    visibility: [],
  }),
  computed: {
    aligning() {
      return "justify-" + this.alignment;
    },
  },
  methods: {
    getTagLengths() {
      for (let i = 0; i < this.tags.length; i++) {
        this.tagLengths.push(
          document.getElementById(i.toString()).getBoundingClientRect().width *
            1.05
        );
      }
    },
    getScreenSize() {
      this.viewSize = document.documentElement.clientWidth;
    },
    isTagVisible() {
      let totalLengths = 0;
      let i = 0;
      while (totalLengths < this.viewSize && i < this.tagLengths.length) {
        if (totalLengths + this.tagLengths[i] < this.viewSize) {
          totalLengths += this.tagLengths[i];
        } else this.visibility[i] = "d-none";
        i++;
      }
      this.componentKey++;
    },
    resize() {
      this.viewSize = document.documentElement.clientWidth;
      this.visibility = [];
      this.isTagVisible();
    },
  },
  mounted() {
    this.getScreenSize();
    window.addEventListener("resize", this.resize);
    this.getTagLengths();
    this.isTagVisible();
  },
};
</script>

<style lang="scss" scoped>
.tag-row {
  width: auto;
  color: #0808b3;
  > p {
    font-size: 1.2rem;
  }
}
.tag-string {
  height: inherit;
}
</style>
