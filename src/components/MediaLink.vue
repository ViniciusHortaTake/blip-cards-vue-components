<template>
  <div :class="'blip-container media-link ' + document.type.split('/')[0]">

    <blip-image :document="document" :position="position" :date="date" v-if="document.type.indexOf('image') != -1" :editable="editable" :on-save="save" :on-deleted="onDeleted" :deletable="deletable" :on-cancel="onCancel" :editing="editing"/>
    <blip-audio :document="document" :position="position" :date="date" v-else-if="document.type.indexOf('audio') != -1" :editable="editable" :on-save="save" :on-deleted="onDeleted" :deletable="deletable" :on-cancel="onCancel" :editing="editing"/>
    <blip-video :document="document" :position="position" :date="date" @updated="emitUpdate" v-else-if="document.type.indexOf('video') != -1" :editable="editable" :on-save="save" :on-deleted="onDeleted" :deletable="deletable" :on-cancel="onCancel" :editing="editing"/>
    <blip-file :document="document" :position="position" :date="date" v-else :editable="editable" :on-save="save" :on-deleted="onDeleted" :deletable="deletable" :on-cancel="onCancel" :editing="editing"/>

    <div :class="'notification ' + position" v-if="date">
      {{ date }}
    </div>
  </div>
</template>

<script>

import BlipImage from './MediaLink/Image'
import BlipAudio from './MediaLink/Audio'
import BlipVideo from './MediaLink/Video'
import BlipFile from './MediaLink/BlipFile'
import { default as base } from '../mixins/baseComponent.js'

export default {
  name: 'media-link',
  mixins: [
    base
  ],
  components: {
    BlipImage,
    BlipAudio,
    BlipVideo,
    BlipFile
  },
  methods: {
    emitUpdate () {
      this.$emit('updated')
    }
  }
}
</script>

<style lang="scss">
   @import '../styles/variables.scss';

</style>
