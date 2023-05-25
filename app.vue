<template>
  <div>
    <Input class="vorname" label="Test label" v-model:value="vorname" :mandatory="true" :deactivated="false" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      vorname: 'Moritz'
    }
  },

  watch: {
    vorname: function (val) {
      console.log(val)
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter&display=swap');

html {
  background-color: rgba(66, 97, 98, 0.06);
}

.vorname {
  width: 270px;
}
</style>