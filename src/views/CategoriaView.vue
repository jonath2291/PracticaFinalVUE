<style>
table,
th,
td {
  padding: 10px;
  border: 1px solid black;
  border-collapse: collapse;
}
</style>
<template>
    
    <div class="Categorias">
        
            Categorias
        <form @submit.prevent="$event =>CrearCategoria()">
            <input type="text" v-model="payload.nombre_categoria" placeholder="titulo">
            <button type="submit">Agregar</button>
            
        </form>
        <p></p>
        

        <table border="1" class="table" align="center">
            <thead>
              <tr>
                <th scope="col">Id</th>
                <th scope="col">Categoria</th>
                <th scope="col">accion</th>
                

                
              </tr>
            </thead>
            <tbody>
              <tr v-for="(value, key) in nombre_categoria" id="key">
                <th scope="row">{{ value.id }}</th>
                <td>{{ value.nombre_categoria }}</td>
                <td><button type="button" class="btn-primary" @click="editar (value)">editar</button>
                <button type="button" class="btn-danger" @click="eliminar (value)">eliminar</button></td>
                
              </tr>
        
            </tbody>
          </table> 
       

    </div>
</template>


<script>
export default {
        name:'CategoriaView',
        props:[],
        emits:[],
        data(){
            return{
                nombre_categoria:[],
                payload:{
                nombre_categoria:""
                }
            }
        },
        methods:{
            getCategoria(){
                this.axios.get("http://localhost:5000/categoria")
                .then((response)=>{
                    this.nombre_categoria=response.data;
                    console.log(response);})

                .catch((err)=>{console.log(err);})
            },
            CrearCategoria(){
                this.axios.post("http://localhost:5000/categoria",this.payload)
                .then((response)=>(this.getCategoria()))
                .catch((err)=>{console.log(err);})

            },
            editar (item){

            },
            eliminar(item){
                this.axios.delete("http://localhost:5000/categoria/"+item.id)
                .then((response)=>{
                    this.getCategoria();
                    console.log(response);})

                .catch((err)=>{console.log(err);})

            }

        },
        computed:{},
        mounted(){
            this.getCategoria();
        },
        components:{}

    }

    
</script>