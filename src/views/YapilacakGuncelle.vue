<template>
  <h1>Yapilacak güncelle</h1>
  <form action="" @submit.prevent="handleSubmet">
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
            icerik:'',
            uri:'http://localhost:3000/yapilacaklar/'+this.id
        }
    },
    mounted(){
      fetch(this.uri)
        .then((res)=>res.json())
        .then(data=>{
          this.baslik=data.baslik;
          this.icerik=data.icerik
        })
    },
    methods:{
      handleSubmet(){
        fetch(this.uri,{
          method:'PATCH',
          headers:{'Content-Type':'application/json'},
          body:JSON.stringify({baslik:this.baslik,icerik:this.icerik})
        }).then(()=>{
          this.$router.push('/')
        }).catch((err)=>console.log(err))
      }
    }
}
</script>

<style>

</style>