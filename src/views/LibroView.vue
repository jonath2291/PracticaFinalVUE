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
    
    <div class="Libros">
        
            Lista de Libros
        <form @submit.prevent="$event =>CrearLibro()">
            <input type="text" v-model="payload.titulo" placeholder="titulo">
            <input type="text" v-model="payload.autor" placeholder="autor">
            <input type="text" v-model="payload.editorial" placeholder="editorial">
            <input type="text" v-model="payload.numeropaginas" placeholder="numero de paginas">
            <input type="text" v-model="payload.ano_publicacion" placeholder="año de publicacion">
            <input type="text" v-model="payload.id_categoria" placeholder="categoria">
            <button type="submit">Agregar</button>
            
        </form>
        <p></p>
        Buscar Libros
        <form @submit.prevent="$event =>BuscarLibro()">
            <input type="text" v-model="payload.titulo" placeholder="titulo">
            <button type="submit">Buscar</button>
            
        </form>
        <p></p>
        <table border="1" class="table" align="center">
            <thead>
              <tr>
                <th scope="col">Id</th>
                <th scope="col">titulo</th>
                <th scope="col">autor</th>
                <th scope="col">editorial</th>
                <th scope="col">numero de paginas</th>
                <th scope="col">año de publicacion</th>
                <th scope="col">categoria</th>
                <th scope="col">accion</th>
                

                
              </tr>
            </thead>
            <tbody>
              <tr v-for="(value, key) in libros" id="key">
                <th scope="row">{{ value.id }}</th>
                <td>{{ value.titulo }}</td>
                <td>{{ value.autor }}</td>
                <td>{{ value.editorial }}</td>
                <td>{{ value.numeropaginas }}</td>
                <td>{{ value.ano_publicacion }}</td>
                <td>{{ value.id_categoria }}</td>
                <td><button type="button" class="btn-primary" @click="editar (value)">editar</button>
                <button type="button" class="btn-danger" @click="eliminar (value)">eliminar</button></td>
                
              </tr>
        
            </tbody>
          </table> 
       

    </div>
</template>


<script>
export default {
        name:'LibroView',
        props:[],
        emits:[],
        data(){
            return{
                libros:[],
                payload:{
                titulo:"",
                autor:"",
                editorial:"",
                numeropaginas:"",
                ano_publicacion:"",
                id_categoria:""
                }
            }
        },
        methods:{
            getLibros(){
                this.axios.get("http://localhost:5000/libro")
                .then((response)=>{
                    this.libros=response.data;
                    console.log(response);})

                .catch((err)=>{console.log(err);})
            },
            BuscarLibro(){
                //this.axios.get("http://localhost:5000/libro?titulo="+this.payload.titulo)
                
                    this.axios.get("http://localhost:5000/libro",{params:{
                        titulo:this.payload.titulo
                
                
                }})
            


                    
                .then((response)=>{
                    this.libros=response.data;
                    
                    console.log(response);})

                .catch((err)=>{console.log(err);})
            },
            CrearLibro(){
                this.axios.post("http://localhost:5000/libro",this.payload)
                .then((response)=>(this.getLibros()))
                .catch((err)=>{console.log(err);})

            },
            editar (item){

            },
            eliminar(item){
                this.axios.delete("http://localhost:5000/libro/"+item.id)
                .then((response)=>{
                    this.getLibros();
                    console.log(response);})

                .catch((err)=>{console.log(err);})

            }

        },
        computed:{},
        mounted(){
            this.getLibros();
        },
        components:{}

    }

    
</script>