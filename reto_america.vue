<template>
    <div>
        <div v-if="cambiopagina==0">
            <button @click="abrirNuevoMaterial()">
                Nuevo Material
            </button>
        </div>
        <div v-if="cambiopagina==1">
            <div class="card card-header">
                Nuevo Material
            </div>
            <div class="card card-body">
                <div class="form-group row">
                    <h4>TÍTULOS DEL MATERIAL</h4><br>
                    <div class="input-group">
                        <label for="">Titulo Original:</label>
                        <input type="text" v-model="titulo_original">
                    </div>
                    <div class="input-group">
                        <label for="">Titulo en español y/o sugerido:</label>
                        <input type="text" v-model="titulo_sugerido">
                    </div>
                    <div class="input-group">
                        <label for="">Titulo Comercial</label>
                        <input type="text" v-model="titulo_comercial">
                    </div>
                </div>
                <div class="form-group row">
                    <h4>DURACIÓN DEL MATERIAL</h4><br>
                    <div class="input-group">
                        <label for="">Duracion:</label>
                        <input type="number" v-model="horas">h
                        <input type="number" v-model="minutos">min
                    <h4>CAPITULOS DEL MATERIAL</h4><br>
                        <input type="number" v-model="segundos">s
                    </div>
                </div>
                <div class="form-group row">
                    <i style="color=red;">Solo llenar si el material tiene captitulos</i>
                    <div class="input-group">
                        <label for="">Temporada:</label>
                        <input type="number" v-model="temporada">
                        <label for="">N° de Capitulos:</label>
                        <input type="number" v-model="capitulos">
                    </div>
                </div>
                <div class="form-group row">
                    <h4>CARACTERISTICAS DEL MATERIAL</h4><br>
                    <div class="input-group">
                        <label for="">Tipo de material:</label>
                        <select v-model="tipo_material">
                            <option value="produccion_nacional">Produccion Nacional</option>
                            <option value="fusion_gourmet">Fusion gourmet</option>
                            <option value="otros">otros</option>
                        </select>
                    </div>
                    <div class="input-group">
                        <label for="">Tipo de contenido:</label>
                        <select v-model="tipo_contenido">
                            <option value="serie">Serie</option>
                            <option value="novela">Novela</option>
                            <option value="mini_serie">Mini serie</option>
                        </select>
                    </div>7
                    <div class="input-group">
                        <label for="">Centro de costo:</label>
                        <select v-model="centro_costo">
                            <option value="001526">001526</option>
                            <option value="001563">001563</option>
                            <option value="001489">001489</option>
                        </select>
                    </div>
                    <div class="input-group">
                        <label for="">Género del material:</label>
                        <select v-model="genero_material">
                            <option value="comedia">Comedia</option>
                            <option value="drama">Drama</option>
                            <option value="accion">Acción</option>
                        </select>
                    </div>
                    <div class="input-group">
                        <label for="">Clasificación:</label>
                        <select v-model="clasificacion">
                            <option value="may_14">MAY 14</option>
                            <option value="todos">apto para todos</option>
                            <option value="may_18">MAY 18</option>
                        </select>
                    </div>
                </div>
                <div class="form-group row">
                    <h4>CANAL DE TRANSMISIÓN</h4><br>
                    <div class="input-group">
                        <label><input type="checkbox" id="cbox1" value="america_tv" v-model="canal"> América TV</label><br>
                        <input type="checkbox" id="cbox2" value="america_next" v-model="canal"> <label for="cbox2">América Next</label>
                    </div>
                </div>
                <div class="form-group row">
                    <button type="button" @click="regresarPaginaPrincipal()">
                        Cancelar
                    </button>
                    <button type="button" @click="enviarMaterial()">
                        Ingresar
                    </button>,
                </div>
            </div>
        </div>

    </div>
</template>
<script>
    export default {
        data (){
            return {
                cambiodepagina: 0,
                titulo_original: "",
                titulo_sugerido: "",
                titulo_comercial: "",
                horas: "",
                minutos: "",
                segundos: "",
                temporada: "",
                capitulos: "",
                tipo_material: "",
                tipo_contenido: "",
                centro_costo: "",
                genero_material: "",
                clasificacion: "",
                canal : [],
            }
        },
        computed:{
        },
        methods : {
            listarPagina(){

            },
            abrirNuevoMaterial(){
                this.cambiodepagina = 1;
            },
            enviarMaterial(){
                axios.post('http://localhost/8000/ejemplo',{
                    
                    'id_categoria': this.titulo_original,
                    'id_presentacion': this.titulo_sugerido,
                    'id_laboratorio': this.titulo_comercial,
                    'codigo': this.horas,
                    'minutos': this.minutos,
                    'segundos': this.segundos,
                    'temporada': this.temporada,
                    'capitulos': this.capitulos,
                    'tipo_material': this.tipo_material,
                    'tipo_contenido': this.tipo_contenido,
                    'centro_costo': this.centro_costo,
                    'genero_material': this.genero_material,
                    'clasificacion': this.clasificacion,
                    'canal': this.canal,
                }).then(function (response) {
                    me.regresarPaginaPrincipal();
                }).catch(function (error) {
                    console.log(error);
                });
            },
            regresarPaginaPrincipal(){
                this.cambiodepagina = 0;
            }
        },
        mounted() {
            this.listarPagina();
        }
    }
</script>
