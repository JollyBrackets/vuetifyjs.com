<template lang="pug">
  component(:is="component" :source="source")
</template>

<script>
  export default {
    data: () => ({
      component: null
    }),

    computed: {
      source () {
        const path = this.$route.fullPath
        return `https://github.com/vuetifyjs/docs/blob/master${path}.vue`
      }
    },

    beforeRouteEnter (to, from, next) {
      return import(
        /* webpackChunkName: "examples" */
        /* webpackMode: "lazy-once" */
        `../examples/${to.params.example}.vue`
      ).then(comp => {
        next(vm => vm.component = comp.default)
      }).catch(e => {
        next('/404')
      })
    }
  }
</script>
