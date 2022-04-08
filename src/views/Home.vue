<template>
  <div>
    <div class="Head">
      Sound Pad ทำมือ v.0.0.2
    </div>
    <div class="column is-8 is-offset-2">
      <draggable :list="favs" group="sound" class="favorite" @change="log">
        <c-button
          class="is-info" v-for="(sound, index) in favs"
          :key="`fav-${index}`"
          :text="sound.th"
          :sound="sound" />
      </draggable>
    </div>
    <div class="column is-8 is-offset-2">
      <draggable :list="sounds" group="sound" class="favorite">
        <c-button
          class="is-info" v-for="(sound, index) in sounds"
          :key="`fav-${index}`"
          :text="sound.th"
          :sound="sound"/>
      </draggable>
    </div>
  </div>
</template>

<script lang="ts">  
import draggable from 'vuedraggable'
import CButton from '@/components/c-button.vue'
import { Component, Vue } from 'vue-property-decorator'
import sounds from '@/utils/sound.json'

@Component({
  components: {
    draggable,
    CButton
  }
})
export default class Home extends Vue {
  private sounds: unknown[] = sounds
  private favs: unknown[] = []

  log (): void {
    window.localStorage.setItem('fav_sound', JSON.stringify(this.favs))
  }

  setFavs (): void {
    const favString = window.localStorage.getItem('fav_sound')
    if (favString) {
      this.favs = JSON.parse(favString)
    }
  }

  mounted (): void {
    this.setFavs()
  }
}
</script>

<style scoped>
.favorite {
  margin-top: 20px;
  border: 2px dashed #cfcfcf;
  border-radius: 18px;
  min-height: 200px;
  display: flex;
  padding: 20px;
  flex-wrap: wrap;
}
</style>
