<template>
  <div>
    <current-user>
      <template v-slot:default="slotProps">
        {{ slotProps.user.firstName }}
      </template>
    </current-user>
    <template v-for="(item, index) in levelList">
      <anchored-heading :level="item" :key="index">-Hello +World!</anchored-heading>
    </template>
  </div>
</template>
<script>
import CurrentUser from '@/components/SlotScope'
import Vue from 'vue'

var getChildrenTextContent = function (children) {
  return children.map(function (node) {
    return node.children
      ? getChildrenTextContent(node.children)
      : node.text
  }).join('')
}

Vue.component('anchored-heading', {
  render: function (createElement) {
    // 创建 kebab-case 风格的 ID
    // console.log(getChildrenTextContent(this.$slots.default).toLowerCase().match(/\W+/g))
    console.log(getChildrenTextContent(this.$slots.default).toLowerCase().replace(/\W+/g, '-'))
    console.log(getChildrenTextContent(this.$slots.default).toLowerCase().replace(/\W+/g, '-').match(/(^-|-$)/g))
    var headingId = getChildrenTextContent(this.$slots.default)
      .toLowerCase()
      .replace(/\W+/g, '-')
      .replace(/(^-|-$)/g, '')

    return createElement(
      'h' + this.level,
      [
        createElement('a', {
          attrs: {
            name: headingId,
            href: '#' + headingId
          }
        }, this.$slots.default)
      ]
    )
  },
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})

export default {
  components: { CurrentUser },
  data () {
    return {
      levelList: [1, 2, 3, 4, 5]
    }
  }
}
</script>
<style lang='less' scoped></style>
