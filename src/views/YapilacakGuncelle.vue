<template>
  <h1>Yapilacak güncelle</h1>
  <form action="" @submit.prevent="">
    <label for="">Baslik:</label>
    <input type="text" v-model="baslik">
    <label for="">içerik:</label>
    <input type="text" v-model="icerik">
    <button>Güncelle</button>
  </form>
</template>

<script>
export default {
    props:['id'],
    data() {
        return {
            baslik:'',
            icerik:''
        }
    },
}
</script>

<style>

</style>