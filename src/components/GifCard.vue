<template>
    <div class="gifCard" @click="copyToClipboard">
        <div class="card">
            <div class="card-image">
                <figure class="image is-4by3">
                  <img v-if="!isCopied" :src="url" alt="Le gif est cassé">
                  <img v-else src="@/assets/succes.png" alt="Succes">
                </figure>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'GifCard',
  data() {
    return {
      isCopied : false
    }
  },
  props: {
    url: String
  },
  methods : {
    copyToClipboard() {
      navigator.clipboard.writeText(this.url).then(() => {
          this.isCopied = true
          console.log('Async: Copying to clipboard was successful!');
          setTimeout(() => {
            this.isCopied = false
          }, 1000)
        }, (err) => {
          console.error('Async: Could not copy text: ', err);
        });
    }
  },
  beforeMount() {
    this.displayedUrl = this.url
  }
}
</script>

<style scoped>
.gifCard { cursor: pointer; }
</style>