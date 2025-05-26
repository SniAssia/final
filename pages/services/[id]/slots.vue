<template>
  <div  class="elem">
   
    <div class="service-list">
        <div v-for="slot1 in reserved" :key="slot1.id" class="service-card">
            <h3>"this service is not available {{ slot1.dateTime }}</h3>
            <p>"this service is already booked"</p>
        </div>
        <div v-for="slot2 in nonreserved" :key="slot2.id" class="service-card">
            <h3>"this service is available {{ slot2.dateTime }}</h3>
            <p>"this service is available"</p>
            <NuxtLink :to="'/book/' + slot2.id " class="button">BOOK THIS SERVICE</NuxtLink>
        </div>
    </div>
</div>
  
</template>
<script>
export default {
    data(){
        return {
            slots : [],
            available:[],
            nonreserved:[],
            reserved:[]
        }
    },
    mounted(){
        this.fetchslots();
    },
    methods : {
        async fetchslots(){
            const id="srv001";
            const res = await fetch("http://localhost:3000/slots");
            this.slots = await res.json();
            console.log(this.slots);
            for (const elem of this.slots){
                if (elem.serviceId==id){
                    this.available.push(elem);
                }
            }
            for (const elem of this.available){
                if (elem.isBooked==true){
                    this.reserved.push(elem);
                }
                else {
                    this.nonreserved.push(elem); 
                }
            }

        }
    }
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

