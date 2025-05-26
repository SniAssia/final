<template>
    <div class="elem">
        <h1>{{ service.name }}</h1>
        <div class="service-list">
        <p>{{ service.description }}</p>
        <p><strong>Durée :</strong> {{ service.duration }} min</p>
        </div>
        <NuxtLink :to="'/services/' + service.id +'/slots'" class="button">Voir les horaires</NuxtLink>
        
    </div>

</template>
<script>
export default {
    data(){
        return {
            service :{},
        }
    }, 
    mounted()  {
        this.fetchbyid();
    },
    methods : {
        async fetchbyid(){
            const id = this.$route.params.id; 
            const res = await fetch(`http://localhost:3000/services/${id}`);
            this.service= await res.json(); 
        }
    }
}
</script>

<style scoped>
.service-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  flex-direction: column;
}
.service-card {
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  width: 300px;
}
.elem {
    display:flex; 
    flex-direction: column;
    font-size: 20px;
    background-color: aqua;
    border-radius: 5px;
    padding: 20px;
    width:600px;
    margin: 40px;
    
}
</style>


