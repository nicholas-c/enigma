<template>
  <div class="mt-6">
    <h2 class="text-xl  mb-4" v-on:click="toggleSettings()">
      Settings
    </h2>

    <div class="settings" :class="{'open' : settings === true }" >
      <div class="w-1/3  mx-auto  flex  flex-wrap  mb-4  justify-center">
        <div class="w-full  mb-4">
          <p>
            With the Enigma machine, each rotor could be swapped around to have different results each time. This setting is to change the rotor, not the values.
          </p>
        </div>

        <div class="w-1/4  px-2" v-for="i in 3" :key="i">
          <label class="w-full  inline-block  mb-2" :for="`rotor-${i}`">
            Rotor {{i}}
          </label>

          <select class="w-full  border  border-black  text-center" :id="`rotor-${i}`">
            <option>I</option>
            <option>II</option>
            <option>III</option>
            <option>IV</option>
            <option>V</option>
            <option>VI</option>
            <option>VII</option>
            <option>VIII</option>
          </select>
        </div>
      </div>

      <div class="w-1/3  mx-auto  flex  flex-wrap  mb-4">
        <div class="w-full  mb-4">
          <p>
           The reflector was at the end of rotors and returned a different value back through the rotors again.
          </p>
        </div>

        <div class="w-full">
          <label>
            Reflector
          </label>

          <select class="border  border-black">
            <option>B</option>
            <option>C</option>
          </select>
        </div>
      </div>
    </div>

    <div class="rotors">
      <Rotor />
    </div>

    <div class="w-1/3  mx-auto  flex  flex-wrap  mb-4">
      <div class="w-full  mb-4">
        Input: <input class="border" />
      </div>

      <div class="w-full">
        Output: <span></span>
      </div>
    </div>
  </div>
</template>

<script>
import Rotor from './Rotor'

export default {
  components: {
    Rotor
  },
  data () {
    return {
      settings: false
    }
  },
  methods: {
    toggleSettings: () => {
      this.settings = !this.settings
    }
  }
}
</script>

<style scoped>
  .settings {
    max-height: 500px;
    transition: 500ms max-height;
  }
  .settings.open {
    max-height: 0;
  }
</style>
