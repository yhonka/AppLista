<template>

    <div class="banner">
      <img
        class="banner-img"
        src="../../public/images/bg-header-desktop.svg" />
    </div>

   <div class="contenedor-f" v-if="this.arrayfilter.length != 0">
    <ul class="contenedor-filter">
      <li v-for="item in arrayfilter" :key="item"  >
        <h3 class=" button boton-filter">{{item}} <span @click="removefilter(item)" class="button cancelar" > X</span></h3>
      </li>
    </ul>
   
      <li class="contenedor-filter-de" >
      <span class="button cancelar" @click="deleter"> Clear</span></li>
   
    
   </div>

    <div class="contenedor" v-for="item in filterdata" :key="item.id"> 
      <div class="conten-izq" >
        <ul>
          <li><img :src="item.logo"/></li>
          <div class="datos">
            <li><h5 class="title">{{item.company}}</h5></li>
            <li><h3  class=" button button2" v-if="item.new">New!</h3></li>
            <li><h3  class=" button button3" v-if="item.featured">Featured</h3></li>
            <h1>{{item.position}}</h1>
            <h2>{{item.postedAt}} · {{ item.contract}} · {{item.location}} </h2>
          </div> 
        </ul>
      </div>

      <div class="conten-dec">
        <ul>
         <li><h3 class="button button1" @click="addfilter(item.role)">{{item.role}}</h3></li>
         <li><h3 class="button button1" @click="addfilter(item.level)" >{{item.level}}</h3></li>
         <li v-for="languages in item.languages" :key="item.languages" ><h3 class="button button1" @click="addfilter(languages)">{{languages}}</h3></li>
         <li v-for="tools in item.tools" :key="item.tools"><h3  class="button button1" @click="addfilter(tools)">{{tools}}</h3></li>
        </ul>
      </div>
    </div>
</template>

<script>

import jsonData from '@/data.json'

export default {
  name: 'MainComponent',
  data () {
    return {
      data: jsonData,
      arrayfilter:[]
    }
  },
  methods:{
    addfilter(newdata){
      if (!this.arrayfilter.includes(newdata)) {
        this.arrayfilter.push(newdata);
      }
    },
    removefilter(removedata){
      this.arrayfilter = this.arrayfilter.filter(word => word != removedata );
    },
    deleter(){
      for (let i = this.arrayfilter.length; i >= 0; i--) {
        var indice = this.arrayfilter.indexOf(this.arrayfilter[i]);
        if (indice != -1)
          this.arrayfilter.splice(indice, 1);
      }
    }
  },
  computed:{
    filterdata(){
			let dataReturn = this.data;
      let filterKey;
      for (let index = 0; index < this.arrayfilter.length; index++) {
        filterKey = this.arrayfilter[index] && this.arrayfilter[index].toLowerCase()
        if (filterKey) {
				  dataReturn = dataReturn.filter(function (row) {
				    return Object.keys(row).some(function (key) {
				      return String(row[key]).toLowerCase().indexOf(filterKey) > -1 
				    })
			 	  })
			  }
      }
      return dataReturn;
    },

  },

}
</script>

<style>
* { 
    margin: 0;
    padding: 0;
    border: 0;
    box-sizing: border-box;
    list-style: none;
    text-decoration: none;  
}
.contenedor{
    width: 80%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    border-radius: 2px;
    padding: 2px 10px;
    margin: 30px 10%;
    background-color: white;
    box-shadow: 0 2px 4px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
}

.conten-izq{
  margin: 1.4rem 0 2.5rem 0;
  text-align: left;
  padding-left: 1%;
}

.datos{
  margin: -5rem 0 0 0;
  text-align: left;
  padding-left: 7rem; 
}

.conten-dec{
  margin: 3rem 0 0 0;
  text-align: left;
}

.contenedor-f{
  position: relative;
  border-radius: 2px;
  margin: -5% 10% 3%;
  background-color: white;
  box-shadow: 0 2px 4px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
  display: grid;
  grid-template-columns: 3fr 1fr;
}

.contenedor-filter{
  margin: 1rem 2rem;
  text-align: left;
}

.contenedor-filter-de{
  margin: 1.7rem 3rem;
  text-align: right;
}

.banner{
  background-color: hsl(180, 29%, 50%);
}

.banner img{
  max-width: 100%;
  height: auto;
}

h1, h5 {
  font-weight: bold;
  font-size: 17px;
}

h2{
  font-weight: bold;
  font-size: 12px;
  color:#919293;
}

.title{
  color: hsl(180, 29%, 50%);
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 3px;
  
}

h3{
  color: hsl(180, 29%, 50%);
  text-decoration: none;
  font-weight: bold;
}

/* Botones */
.button {
  
  border-radius: 2px;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 13px;
  margin: 3px 1px;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
  cursor: pointer;
}

.button1 {
  background-color: hsla(180, 10%, 75%, 0.288);
  color: hsl(180, 29%, 50%);
}

.button1:hover {
  text-decoration: none;
  background-color:hsl(180, 29%, 50%);
  color: white;
}

.button2{
  border-radius: 70px;
  background-color: hsl(180, 29%, 50%);
  color: white;
  cursor:default;
    
}

.button2:hover {
  text-decoration: none;
  background-color: hsla(180, 10%, 75%, 0.288);
  color: hsl(180, 29%, 50%);
  
}

.button3{
  border-radius: 70px;
  background-color: hsl(180, 14%, 20%);
  color: white;
  cursor:default;
    
}

.button3:hover {
  text-decoration: none;
  background-color: hsla(180, 10%, 75%, 0.288);
  color: hsl(180, 29%, 50%);
}

.boton-filter{
  margin: 10px;
  background-color: hsla(180, 10%, 75%, 0.288);
  color: hsl(180, 29%, 50%);
}

.cancelar{
  border-radius: 0 2px 2px 0;
  padding-top: 0.4rem;
  margin: -0.5rem -0.6rem -0.3rem 0;
  background-color: hsl(180, 29%, 50%);
  color: white;
  
}

.cancelar:hover {
  text-decoration: none;
  background-color: hsl(180, 14%, 20%);
  
}
 li .clear{
  background: black;
}

@media screen and (max-width: 800px){
    .contenedor {
      grid-template-columns: 1fr;     
    }
    .conten-dec{
      margin: -2rem 0 0 0;
    } 
   
}

@media screen and (max-width: 420px){
    .contenedor-filter{
      margin: 1rem 0;
    }
    .contenedor-filter-de{
      margin: 1rem 2rem; 
    }

   
}
@media screen and (max-width: 300px){
  .contenedor-f{
    display: grid;
    grid-template-columns: 1fr;
  }
}
     
</style>