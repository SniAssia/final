<template>
  <div  class="elem">
    <h1>Nos Services</h1>
    <div class="service-list">
      <div v-for="service in services" :key="service.id" class="service-card">
        <div >
        <h3>{{ service.name }}</h3>
        <p>{{ service.description }}</p>
        <p><strong>Durée :</strong> {{ service.duration }} min</p>
        <NuxtLink :to="'/services/' + service.id" class="button">Voir les détails</NuxtLink>
        </div>
        
      </div>
    </div>
  </div>
</template>
<script>
export default {
    data() {
        return {
            services : [],
        }
    }, 
    mounted(){
        this.fetchservices();
    }, 
    methods : {
        async fetchservices(){
            const res = await fetch("http://localhost:3000/services"); 
            this.services=await res.json();
        }
    },
    
}
</script>

<style scoped>
.service-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
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
    padding: 90px;
    width:400px;
    margin: 40px;
    
}
</style>
