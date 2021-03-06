<template>
  <v-card flat>
    <v-subheader>Style</v-subheader>
    <message-style-table />
    <v-subheader class="mt-5">Visibility</v-subheader>
    <Message-visibility-table />
    <v-subheader class="mt-5">Appearance</v-subheader>
    <div class="px-4">
      <div class="d-flex">
        <v-select
          v-model="heightType"
          :items="heightTypes"
          label="Height"
          dense
          class="pt-3 mr-3 flex-grow-0"
          style="width: 120px;"
        />
        <v-text-field
          v-if="heightType === 'fixed'"
          v-model="lineHeight"
          :placeholder="placeholder.lineHeight"
          label="Line Height"
          type="number"
          dense
          min="1"
          step="2"
          suffix="px"
          class="pt-3"
        />
        <v-text-field
          v-else
          v-model="lines"
          :placeholder="placeholder.lines"
          label="Lines"
          type="number"
          dense
          min="1"
          class="pt-3"
        />
      </div>
      <v-text-field
        v-model="opacity"
        :placeholder="placeholder.opacity"
        label="Opacity"
        type="number"
        dense
        min="0"
        max="1"
        step="0.1"
        class="pt-3"
      />
      <v-textarea
        v-model="extendedStyle"
        :placeholder="placeholder.extendedStyle"
        label="Extended Style"
        dense
        rows="1"
        auto-grow
        class="pt-3"
      />
    </div>
    <v-subheader class="mt-5">Behavior</v-subheader>
    <div class="px-4">
      <v-text-field
        v-model="speed"
        :placeholder="placeholder.speed"
        label="Display Time"
        type="number"
        dense
        min="1"
        max="10"
        step="0.1"
        suffix="sec"
        class="pt-3"
      />
      <v-text-field
        v-model="displays"
        :placeholder="placeholder.displays"
        label="Max Displays (Infinite if set to 0)"
        type="number"
        dense
        min="0"
        class="pt-3"
      />
      <v-select
        v-model="stackDirection"
        :items="stackDirections"
        label="Stack Directions"
        dense
        class="pt-3"
      />
      <v-select
        v-model="overflow"
        :items="overflows"
        label="Overflow Mode"
        dense
        class="pt-3"
      />
      <v-btn class="my-4" depressed block @click="onResetClick">
        Reset Settings to Default
      </v-btn>
    </div>
  </v-card>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import MessageStyleTable from '~/components/MessageStyleTable.vue'
import MessageVisibilityTable from '~/components/MessageVisibilityTable.vue'
import { settingsStore } from '~/store'

@Component({
  components: {
    MessageStyleTable,
    MessageVisibilityTable,
  },
})
export default class MessageTabItem extends Vue {
  placeholder = {
    lines: '12',
    lineHeight: '64',
    opacity: '0.8',
    extendedStyle: 'font-family: "Yu Gothic", YuGothic, Meiryo;',
    speed: '5',
    displays: '0',
  }
  heightTypes = [
    { text: 'Flexible', value: 'flexible' },
    { text: 'Fixed', value: 'fixed' },
  ]
  stackDirections = [
    { text: 'Top to Bottom', value: 'top_to_bottom' },
    { text: 'Bottom to Top', value: 'bottom_to_top' },
  ]
  overflows = [
    { text: 'Hidden', value: 'hidden' },
    { text: 'Overlay', value: 'overlay' },
  ]

  get heightType() {
    return settingsStore.heightType
  }
  set heightType(value) {
    settingsStore.setHeightType({ heightType: value })
  }

  get lines() {
    return settingsStore.lines
  }
  set lines(value) {
    settingsStore.setLines({ lines: Number(value) })
  }

  get lineHeight() {
    return settingsStore.lineHeight
  }
  set lineHeight(value) {
    settingsStore.setLineHeight({ lineHeight: Number(value) })
  }

  get opacity() {
    return settingsStore.opacity
  }
  set opacity(value) {
    settingsStore.setOpacity({ opacity: Number(value) })
  }

  get extendedStyle() {
    return settingsStore.extendedStyle
  }
  set extendedStyle(value) {
    settingsStore.setExtendedStyle({
      extendedStyle: value,
    })
  }

  get speed() {
    return settingsStore.speed
  }
  set speed(value) {
    settingsStore.setSpeed({ speed: Number(value) })
  }

  get displays() {
    return settingsStore.displays
  }
  set displays(value) {
    settingsStore.setDisplays({ displays: Number(value) })
  }

  get stackDirection() {
    return settingsStore.stackDirection
  }
  set stackDirection(value) {
    settingsStore.setStackDirection({ stackDirection: value })
  }

  get overflow() {
    return settingsStore.overflow
  }
  set overflow(value) {
    settingsStore.setOverflow({ overflow: value })
  }

  onResetClick() {
    settingsStore.resetState()
  }
}
</script>
