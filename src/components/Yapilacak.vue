<template>
  <div class="yapilacak" :class="{yapildi:yapilacak.yapildi}">
    <div class="baslik">
        <h3 @click="detaygoster=!detaygoster">{{ yapilacak.baslik }}</h3>
        <div class="icon">
            <router-link :to="{name:'YapilacakGuncelle',params:{id:yapilacak.id}}">
                <i class='bx bx-edit-alt' ></i>
            </router-link>
            <i class='bx bx-trash' @click="yapilacaksil"></i>
            <i class='bx bx-check' @click="toggle"></i>
        </div>
    </div>
    <div v-if="detaygoster" class="detay">
        <p>{{ yapilacak.icerik }}</p>
    </div>
  </div>
</template>

<script>
export default {
    props:['yapilacak'],
    data() {
        return {
            detaygoster:false,
            uri:'http://localhost:3000/yapilacaklar/'+this.yapilacak.id

        }
    },
    methods:{
        yapilacaksil(){
            fetch(this.uri,{method:'DELETE'})
                .then(()=>this.$emit('sil',this.yapilacak.id))
                .catch((err)=>console.log(err))
        },
        toggle(){
            fetch(this.uri,{
                method:'PATCH',
                headers:{'Content-Type':'application/json'},
                body:JSON.stringify({yapildi:!this.yapilacak.yapildi})
            }).then(()=>{
                this.$emit('yapildi',this.yapilacak.id)
            }).catch((err)=>console.log(err))
        }
    }
}
</script>

<style>
.yapilacak{
    margin: 20px auto;
    background:#4b4b4b;
    padding: 10px 20px;
    border-radius: 15px;
    border: 3px solid #b33939;
    color: #f7f1e3;
}
.yapilacak:hover{
    box-shadow: 8px 10px 10px rgba(2, 2, 2, .3);
}
.yapilacak.yapildi{
    border: 3px solid #218c74;
}
.yapilacak.yapildi .tick{
    color: #218c74;
}
h3{
    cursor: pointer;
}
.baslik{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.bx{
    font-size: 25px;
    margin-left: 10px;
    cursor: pointer;
    color: #bbb;
}
.bx:hover{
    color: #2f3542;
}
</style>