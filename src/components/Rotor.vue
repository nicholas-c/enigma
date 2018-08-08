<template>
  <div>
    <select class="border  border-black  capitalize">
      <option
        v-for="i in 26"
        :key="i"
        :value="rotorValues[0][i - 1]"
      >
        {{String.fromCharCode(96 + i)}}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  data () {
    return {
      rotorValues: [
        'EKMFLGDQVZNTOWYHXUSPAIBRCJ',
        'AJDKSIRUXBLHWTMCQGZNPYFVOE',
        'BDFHJLCPRTXVZNYEIWGAKMUSQO',
        'ESOVPZJAYQUIRHXLNFTGKDCMWB',
        'VZBRGITYUPSDNHLXAWMJQOFECK',
        'JPGVOUMFYQBENHZRDKASXLICTW',
        'NZJHGRCXMYSWBOUFAIVLPEKQDT',
        'FKQHTLXOCBJSPDZRAMEWNIUYGV',
      ]
    }
  }
}
</script>
