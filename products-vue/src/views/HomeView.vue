<template>
<div class="row">
    <div class="col-lg-8 offset-lg-2">
        <div class="table-responsive">
            <table class="table table-bordered table-hover">
                <thead><tr><th>#</th><th>NOMBRE</th><th>COMIDA</th><th>FECHA</th></tr></thead>
                <tbody class="table-group-divider" id="contenido">

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
                        this.products = response.data
                    )
                );
            }
        }

    }
</script>

