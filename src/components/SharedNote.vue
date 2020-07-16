<template>
  <div class="col-md-offset-4 col-sm-offset-2 col-md-4 col-sm-8">
    <div class="single-note shared" :class="[sharedNote().color]">
      <h2>{{sharedNote.title}}</h2>
      <small>The Date: {{sharedNote().date}}</small>
      <hr>
      <p v-html="sharedNote().text"></p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SharedNote',
  methods: {
    sharedNote () {
      // Detect Links
      const detectLinks = /((https?:\/\/)(\S+))/g
      const detectLinksWWW = /((www\.)(\S+))/g
      if (this.getParam('note')) {
        const shared = JSON.parse(decodeURIComponent(this.getParam('note')))
        shared.text = shared.text.replace(detectLinks, '<a href="$1" target="_black">$1</a>').replace(detectLinksWWW, '<a href="http://$1" target="_black">$1</a>')
        return shared
      }
    },
    // Define a function to get link parameter
    getParam (query) {
      const param = {}
      let link = window.location.search
      link = link.replace('?', '')
      link.split('&').forEach(function (variable) {
        const half = variable.split('=')
        param[half[0]] = half[1]
      })
      return param[query] || ''
    }
  }
}
</script>
