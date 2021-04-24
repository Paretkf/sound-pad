<template>
  <div>
    <audio id="sound" ref="audio" preload="metadata">
      <source :src="require(`@/assets/sound/${sound.path}`)" type="audio/mpeg" />
    </audio>
    <b-button
    class="is-info btn" @click="toggleSound">
      {{ text }}
    </b-button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'


@Component
export default class CButton extends Vue {
  @Prop()
  readonly text!: string

  @Prop()
  readonly sound!: any

  isPlaying = false

  time = 2

  async toggleSound(sound: any): Promise<void> {
    const audio: any = this.$refs.audio
    audio.play()
    this.isPlaying = true
    setTimeout(() => {
      this.isPlaying = false
    }, this.time * 1000 + 750)
  }
}
</script>
<style scoped>
.btn {
  margin: 5px 5px 5px 5px;
}
</style>