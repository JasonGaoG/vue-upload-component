<template>
  <input v-if="$parent.show" type="file" :name="$parent.name" :id="$parent.inputId || $parent.name" :accept="$parent.accept" :capture="$parent.capture" :disabled="$parent.disabled"
    @change="change" :webkitdirectory="$parent.directory && $parent.features.directory" :directory="$parent.directory && $parent.features.directory" :multiple="$parent.multiple && $parent.features.html5" />
</template>
<script>
export default {
  methods: {
    change (e) {
      this.$parent.addInputFile(e.target)
      e.target.value = ''
      if (!e.target.files) {
        // ie9 fix #219
        this.$destroy()
        // eslint-disable-next-line
        new this.constructor({
          parent: this.$parent,
          el: this.$el,
        })
      }
    }
  }
}
</script>
