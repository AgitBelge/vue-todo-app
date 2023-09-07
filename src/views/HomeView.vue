<template>
  <div class="home">
    <NavbarFilter @filterDurum="aktifSekme=$event" :aktifSekme="aktifSekme"/>
    <div v-if="yapilacaklar.length">
      <div v-for="yap in filtrelenmisYapilacaklar" :key="yap.id">
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
import NavbarFilter from '../components/NavbarFilter'


export default {
  name: 'HomeView',
  components:{
    Yapilacak,
    NavbarFilter
  },
  data() {
    return {    
      yapilacaklar:[],
      aktifSekme:'hepsi'
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
  },
  computed:{
    filtrelenmisYapilacaklar(){
      if(this.aktifSekme==='tamamlandi'){
        return this.yapilacaklar.filter(veri=>veri.yapildi)
      }
      if(this.aktifSekme==='yapiliyor'){
        return this.yapilacaklar.filter(veri=>!veri.yapildi)
      }
      return this.yapilacaklar
    }
  }
}
</script>

