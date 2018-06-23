<template>
  <div popup class="container">
    <input type="text" class="form-control" v-model="keywords">
    <button class="btn btn-info" @click="save">儲存</button>
  </div>
</template>

<script>
import bootstrap from 'bootstrap/dist/js/bootstrap.min.js'
export default {
  data() {
    return {
      keywords: null
    }
  },
  methods: {
    search() {
      chrome.tabs.query({active: true, currentWindow: true}, (tabs) => {
        chrome.tabs.sendMessage(tabs[0].id, {
          formHelper: {
            action: 'search',
          },
        })
      })
    },
    save() {
      alert('save')
      chrome.storage.sync.set({
        keywords: this.keywords,
      })
    }
  },
}
</script>

<style src="bootstrap/dist/css/bootstrap.min.css"></style>
<style src="font-awesome/css/font-awesome.min.css"></style>
<style lang="sass" scoped>
div[popup]
  width: 300px
  height: 200px
  padding: 15px
  &>*
    margin: 10px 0
</style>