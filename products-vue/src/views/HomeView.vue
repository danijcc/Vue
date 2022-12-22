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
                            <button class="btn btn-danger" v-on:click="eliminar(food.id,food.title)">
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
    import {confirmar, show_alerta} from '../funciones';
    import Swal from "sweetalert2";
    
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
            eliminar(id,title){
                const swalWhitBootstrapButton= Swal.mixin({
                    customClass:{
                        confirmButton:'btn btn-success me-3',
                        cancelButton:'btn btn-danger'
                    },
                    buttonsStyling:false
                });

                swalWhitBootstrapButton.fire({
                    title: 'Seguro de eliminar el Item ' + title +" ?",
                    text: 'Se perdera la informacion del producto',
                    icon: 'question',
                    showCancelButton:true,
                    confirmButtonText:'<i class="fa-solid fa-check"></i> Si, eliminar',
                    cancelButtonText:'<i class="fa-solid fa-ban"></i> Cancelar'
                })
                .then((ressult)=>{
                    if(ressult.isConfirmed){
                        axios.delete('http://127.0.0.1:8000/api/foods/'+id)
                        .then( (response) => {
                            let status = response.status;
                            
                            if([200, 201, 204].includes(status)){
                                show_alerta('Se elimino correctamente', 'success');
                                this.getFoods()

                            }else{
                                var listado='';
                                var errores = respuesta.data.data[1]['errors'];
                                Object.keys(errores).forEach(
                                    key => listado += errores[key][0]+'.');
                                    show_alerta(listado,'error');
                            }
                        })
                    }else{
                        show_alerta('Operacion cancelada','info');
                    }
                })
                
            }
        }

    }
</script>

