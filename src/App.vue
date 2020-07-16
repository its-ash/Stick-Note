<template>
  <div id="app">
    <div class="header" id="header" :class="{hash: isHashtag}">
      <div class="container">
        <div class="col-md-3 col-sm-5">
          <a href="/">
            <h2 v-if="isHashtag && !shared"><i style="color:red;" class="fas fa-times"></i> {{getParam.s}}</h2>
            <h2 v-else>Sticky Notes</h2>
          </a>
        </div>
        <div class="col-md-6 col-md-push-3 col-sm-7">
          <div class="hold-img">
            <img v-if="isHashtag && !shared" src="../public/img/Group 13.svg" alt="">
            <img v-else-if="shared && !isHashtag" src="../public/img/Group 12.svg" alt="">
            <img v-else src="../public/img/Group 10.svg" alt="">
          </div>
        </div>
      </div>
    </div>
    <div id="notes" class="notes">
      <div class="container">
        <SharedNote v-if="shared"></SharedNote>
        <MultiNote v-else></MultiNote>
      </div>
    </div>

    <footer>
      <div class="container">
        <span>Made With <i class="fas fa-heart"></i> In <a href="https://neofox.in/">NeoFox</a></span>
      </div>
    </footer>

  </div>
</template>

<script>
import MultiNote from './components/MultiNote'
import SharedNote from './components/SharedNote'

export default {
  name: 'App',
  components: {
    MultiNote,
    SharedNote
  },
  data () {
    return {
      shared: window.location.search.includes('note'),
      isHashtag: window.location.search.includes('s=')
    }
  },
  computed: {
    getParam () {
      const param = {}
      let link = window.location.search
      link = link.replace('?', '')
      link.split('&').forEach(function (variable) {
        const half = variable.split('=')
        param[half[0]] = half[1]
      })
      return param
    }
  }
}
</script>
