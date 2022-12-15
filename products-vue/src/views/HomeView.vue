<template>
<div class="row">
    <div class="col-lg-8 offset-lg-2">
        <div class="table-responsive">
            <table class="table table-bordered table-hover">
                <thead><tr><th>#</th><th>NOMBRE</th><th>FECHA</th><th>FECHA2</th><th>ACCIONES</th></tr></thead>
                <tbody class="table-group-divider" id="contenido">
                    <tr v-for="food, i in foods" :key="food.id">
                        <td>{{food.id}}</td>
                        <td>{{food.title}}</td>
                        <td>{{food.created_at}}</td>
                        <td>{{food.updated_at}}</td>
                        <td>
                            <router-link :to="{path:'edit/'+food.id}" class="btn btn-warning">
                                <i class="fa-solid fa-edit"></i>
                            </router-link>&nbsp;
                            <button class="btn btn-danger">
                                <i class="fa-solid fa-trash"></i>
                            </button>
                        </td>
                    
                    </tr>
                </tbody>
            </table>
        </div> 
    </div>
</div>
</template>
<script>
    import axios from "axios";
    export default{
        data(){
            return {foods:null}
        },
        mounted(){
            this.getFoods();
        },
        methods:{
            getFoods(){
                axios.get('http://127.0.0.1:8000/api/foods').then(
                    response =>(
                        this.foods = response.data.data
                    )
                );
            },
            eliminar(id,nombre){
                
            }
        }

    }
</script>

