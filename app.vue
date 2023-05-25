<template>
  <div class="main">
    <Input class="vorname" label="Geschätztes Lieferdatum" type="date" v-model:value="vorname" :mandatory="false"
      :disabled="false" />
    <Input class="vorname" label="Test 2" v-model:value="test" :mandatory="true" :disabled="false" />
    <Input class="vorname" label="Test 2" v-model:value="three" :mandatory="true" :disabled="false" />
    <!-- <InputDropdown class="vorname" label="Test dropdown" v-model:value="test" :mandatory="true" :disabled="false" /> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      vorname: '',
      test: '6363 378t3',
      three: '',
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

.main {
  display: flex;
  flex-flow: column;
  gap: 12px;
}

.vorname {
  width: 270px;
}
</style>