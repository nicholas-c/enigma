<template>
  <div class="mt-6">
    <h2 class="text-xl  mb-4" v-on:click="toggleSettings()">
      Settings
    </h2>

    <div class="settings" :class="{'open' : settings === true }" >
      <div class="w-1/3  mx-auto  flex  flex-wrap  flex-row-reverse  mb-4  justify-center">
        <div class="w-full  mb-4">
          <p>
            With the Enigma machine, each rotor could be swapped around to have different results each time. This setting is to change the rotor, not the values.
          </p>
        </div>

        <div class="w-1/4  px-2">
          <label class="w-full  inline-block  mb-2" for="rotor-1">
            Rotor 1
          </label>

          <select v-model="rotorSettings[0]" class="w-full  border  border-black  text-center" id="rotor-1">
            <option value="0" selected="selected">I</option>
            <option value="1">II</option>
            <option value="2">III</option>
            <option value="3">IV</option>
            <option value="4">V</option>
            <option value="5">VI</option>
            <option value="6">VII</option>
            <option value="7">VIII</option>
          </select>
        </div>

        <div class="w-1/4  px-2">
          <label class="w-full  inline-block  mb-2" for="rotor-1">
            Rotor 2
          </label>

          <select v-model="rotorSettings[1]" class="w-full  border  border-black  text-center" id="rotor-1">
            <option value="0">I</option>
            <option value="1" selected="selected">II</option>
            <option value="2">III</option>
            <option value="3">IV</option>
            <option value="4">V</option>
            <option value="5">VI</option>
            <option value="6">VII</option>
            <option value="7">VIII</option>
          </select>
        </div>

        <div class="w-1/4  px-2">
          <label class="w-full  inline-block  mb-2" for="rotor-1">
            Rotor 3
          </label>

          <select v-model="rotorSettings[2]" class="w-full  border  border-black  text-center" id="rotor-1">
            <option value="0">I</option>
            <option value="1">II</option>
            <option value="2" selected="selected">III</option>
            <option value="3">IV</option>
            <option value="4">V</option>
            <option value="5">VI</option>
            <option value="6">VII</option>
            <option value="7">VIII</option>
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

    <div class="rotors  w-1/3  mx-auto  flex  flex-wrap  flex-row-reverse  mb-4">
      <div class="w-1/3  px-4">
        <select class="w-full  text-center  border  border-black" v-model="rotors[0]">
          <option
            v-for="i in 26"
            :key="i"
            :value="i - 1"
          >
            {{String.fromCharCode(64 + i)}}
          </option>
        </select>
      </div>

      <div class="w-1/3  px-4">
        <select class="w-full  text-center  border  border-black" v-model="rotors[1]">
          <option
            v-for="i in 26"
            :key="i"
            :value="i - 1"
          >
            {{String.fromCharCode(64 + i)}}
          </option>
        </select>
      </div>

      <div class="w-1/3  px-4">
        <select class="w-full  text-center  border  border-black" v-model="rotors[2]">
          <option
            v-for="i in 26"
            :key="i"
            :value="i - 1"
          >
            {{String.fromCharCode(64 + i)}}
          </option>
        </select>
      </div>
    </div>

    <div class="w-1/3  mx-auto  flex  flex-wrap  mb-4">
      <div class="w-full  mb-4">
        Input: <input v-model="inputValue" class="border" />
      </div>

      <div class="w-full">
        Output: <span>{{outputValue}}</span>
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
      inputValue: '',
      outputValue: '',
      settings: false,
      rotors: {
        0: 0,
        1: 0,
        2: 0
      },
      rotorSettings: {
        0: 0,
        1: 1,
        2: 2
      },
      rotorValues: [
        Array.from('EKMFLGDQVZNTOWYHXUSPAIBRCJ'),
        Array.from('AJDKSIRUXBLHWTMCQGZNPYFVOE'),
        Array.from('BDFHJLCPRTXVZNYEIWGAKMUSQO'),
        Array.from('ESOVPZJAYQUIRHXLNFTGKDCMWB'),
        Array.from('VZBRGITYUPSDNHLXAWMJQOFECK'),
        Array.from('JPGVOUMFYQBENHZRDKASXLICTW'),
        Array.from('NZJHGRCXMYSWBOUFAIVLPEKQDT'),
        Array.from('FKQHTLXOCBJSPDZRAMEWNIUYGV')
      ]
    }
  },
  methods: {
    toggleSettings: () => {
      this.settings = !this.settings
    }
  },
  watch: {
    inputValue () {
      if (this.inputValue !== '') {
        const keypressed = this.inputValue.charCodeAt(0) - 65 >= 32 ? (this.inputValue.charCodeAt(0) - 65) - 32 : this.inputValue.charCodeAt(0) - 65
        let currentValue = this.inputValue

        currentValue = this.rotorValues[this.rotorSettings[0]][keypressed]
        currentValue = this.rotorValues[this.rotorSettings[1]][currentValue.charCodeAt(0) - 65]
        currentValue = this.rotorValues[this.rotorSettings[2]][currentValue.charCodeAt(0) - 65]

        this.rotorValues[this.rotorSettings[0]].push(this.rotorValues[this.rotorSettings[0]].shift())
        this.rotors[0]++

        if (this.rotors[0] === 26) {
          this.rotors[0] = 0
          this.rotors[1]++

          if (this.rotors[1] === 26) {
            this.rotors[1] = 0
            this.rotors[2]++
          }

          if (this.rotors[2] === 26) {
            this.rotors[2] = 0
          }
        }

        this.outputValue = currentValue
      }

      this.inputValue = ''
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
