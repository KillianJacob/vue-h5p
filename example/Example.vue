<template>
  <div class="wrapper" style="width:30%">
    <h5p
      src="/video/"
      content="/video/content/content.json"
      :loadedDepJS="libraryJSBase64Map"
      :loadedDepCSS="libraryCSSBase64Map"
      @loadDependenciesJS="loadedDepJS"
      @loadDependenciesCSS="loadedDepCSS"
      @xapi="log"
      >
      Loading...
      <template v-slot:404="{ response }">
        {{ response.url + ' ' + response.statusText }}
      </template>
    </h5p>
    <button v-on:click="isHidden = false">Load</button>
     <h5p
      v-if="!isHidden"
      src="/video/"
      content="/video/content/content.json"
      :loadedDepJS="libraryJSBase64Map"
      :loadedDepCSS="libraryCSSBase64Map"
      @loadDependenciesJS="loadedDepJS"
      @loadDependenciesCSS="loadedDepCSS"
      @xapi="log"
      >
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
      isHidden: true,
      translations: {
        en: {},
        de: {
          reuse: 'Wiederverwenden',
          reuseContent: 'Content Wiederverwenden'
        }
      },
      libraryCSSBase64Map : [],
      libraryJSBase64Map : []
    }
  },
  async mounted () {
    console.log('Vue-h5p example loaded!')
  },
  methods: {
    log (ev) {
      console.log('catched: ', ev)
    },
    loadedDepJS (libraryJSBase64Map) {
      this.libraryJSBase64Map = libraryJSBase64Map
    },
    loadedDepCSS (libraryCSSBase64Map) {
      this.libraryCSSBase64Map = libraryCSSBase64Map
    }    
  }
}
</script>

<style>
.wrapper {
  height: 98vh;
}
</style>
