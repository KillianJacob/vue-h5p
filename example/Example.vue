<template>
  <div class="wrapper">
    <h5p
      src="/video/"
      content="/video/test"
      @xapi="log"
      :l10n="translations[locale]"
      icon
      copyright
      :key="locale"
      ref="foo">
      Loading...
      <template v-slot:404="{ response }">
        {{ response.url + ' ' + response.statusText }}
      </template>
    </h5p>
  </div>
</template>

<script>
import h5p from '@/h5p'

export default {
  name: 'Example',
  components: {
    h5p
  },
  data () {
    return {
      locale: 'en',
      displayOptions: {
        frame: true,
        copyright: true,
        embed: true,
        icon: true,
        export: true
      },
      translations: {
        en: {},
        de: {
          reuse: 'Wiederverwenden',
          reuseContent: 'Content Wiederverwenden'
        }
      }
    }
  },
  async mounted () {
    console.log('Vue-h5p example loaded!')
  },
  methods: {
    log (ev) {
      console.log('catched: ', ev)
      console.log(this.$refs.foo.path);
    }
  }
}
</script>

<style>
.wrapper {
  height: 98vh;
}
</style>
