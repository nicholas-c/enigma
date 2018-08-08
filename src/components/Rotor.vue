<template>
  <div class="w-1/3">
    <p class="text-xl  mb-4">
      Rotor {{parseInt(selectedRotor) + 1}} loaded
    </p>

    <select class="border  border-black" v-model="rotor[index]">
      <option
        v-for="i in 26"
        :key="i"
      >
        {{String.fromCharCode(64 + i)}}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: ['selectedRotor', 'index'],
  data () {
    return {
    }
  }
}
</script>
