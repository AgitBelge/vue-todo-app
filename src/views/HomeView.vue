<template>
  <div class="home">
    <div v-if="yapilacaklar.length">
      <div v-for="yap in yapilacaklar" :key="yap.id">
      <Yapilacak :yapilacak="yap" @sil="silhandle" @yapildi="yapildihandle"/>
      </div>
    </div>
    <div v-else>
      yapilacaklar yükleniyor
    </div>
  </div>
</template>

<script>
import Yapilacak from '../components/Yapilacak'


export default {
  name: 'HomeView',
  components:{
    Yapilacak
  },
  data() {
    return {    
      yapilacaklar:[]
    }
  },
  mounted() {
    fetch('http://localhost:3000/yapilacaklar')
      .then((res)=>res.json())
      .then((data)=>this.yapilacaklar=data)
      .catch((err)=>console.log(err))
  },
  methods:{
    silhandle(id){
      this.yapilacaklar=this.yapilacaklar.filter(yap=>{
        return yap.id !==id
      });
    },
    yapildihandle(id){
      let yap=this.yapilacaklar.find(osman=>{
        return osman.id==id
      });
      yap.yapildi=!yap.yapildi
    }
  }
}
</script>

