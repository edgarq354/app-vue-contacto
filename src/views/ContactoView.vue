<template>
    <div class="container">

        <h1>{{ title }}</h1>
        <p><button type="button" class="btn btn-primary" @click="goToNew()">Nuevo</button></p>
        <div class="mb-3">
            <div class="input-group">
                <span class="input-group-text" id="basic-addon3">Filtrar por:</span>
                <select v-model="marcaSeleccionado" id="color" class="form-select"> 
                    <option value="">Todos</option>
                    <option v-for="name in names" :key="name" :value="name">
                        {{ name }}
                    </option>
                </select>
            </div>
        </div>
        <div class="mb-3">
            <div class="input-group">
                <span class="input-group-text" id="basic-addon3" >Buscar por {{ marcaSeleccionado }}</span>
                <input type="search" v-model="modeloAbuscar"  class="form-control">
            </div>
        </div>
        <div>
            <table class="table table-bordered border-primary">
                <thead>
                    <tr>
                        <th scope="col">Id</th>
                        <th scope="col">Nombre</th>
                        <th scope="col">Correo Electrónico</th>
                        <th scope="col">Direccion</th>
                        <th scope="col">Telefono</th>
                        <th scope="col">País</th>
                        <th scope="col">Ciudad</th>
                        <th>Acción</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, index) in getItems" :key="item.id">
                        <th scope="row">{{ item.id }}</th>
                        <td>{{ item.name }}</td>
                        <td>{{ item.email }}</td>
                        <td>{{ item.address }}</td>
                        <td>{{ item.phone }}</td>
                        <td>{{ item.country }}</td>
                        <td>{{ item.city }}</td>
                        <td><button type="button" class="btn btn-primary" @click="abrirModal(index)">
                                Editar
                            </button>
                            <button type="button" class="btn btn-danger" @click="eliminar(index)">
                                eliminar
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

    </div>


    <!-- Modal Bootstrap -->
    <div class="modal fade" id="modalContactoEditar" tabindex="-1" aria-labelledby="modalContactoEditarLabel" aria-hidden="true"
        ref="modalRef">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="modalContactoEditarLabel" v-if="modalMode =='editar'" >Editar Contacto</h5>
                    <h5 class="modal-title" id="modalContactoEditarLabel" v-if="modalMode =='crear'" >Crear Contacto</h5> 
                </div>
                <div class="modal-body">
                    <!-- Componente ContactoEditar -->
                    <ContactoEditar v-if="modalMode =='editar' && autoSeleccionado" :auto="autoSeleccionado" @update="guardarEdicion"
                        @cancelar="cerrarModal" />
                    <NuevoContactoView v-if="modalMode =='crear'" @created="agregarNuevo($event)"></NuevoContactoView>    
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import ContactoEditar from '../components/ContactoEditor.vue';
import NuevoContactoView from '../components/NuevoView.vue';
export default {
    name: 'ContactoView',
    data() {
        return {
            title: 'Agenda de Contactos',
            items: [ 
{ 
id: 1, 
name: "Alice Johnson", 
email: "alice.johnson@example.com", 
address: "123 Maple Street", 
phone: "123-456-7890", 
country: "USA", 
city: "New York" 
}, 
{ 
id: 2, 
name: "Bob Smith", 
email: "bob.smith@example.com", 
address: "456 Oak Avenue", 
phone: "987-654-3210", 
country: "Canada", 
city: "Toronto" 
}, 
{ 
id: 3, 
name: "Carol White", 
email: "carol.white@example.com",
address: "789 Pine Road", 
phone: "555-123-4567", 
country: "UK", 
city: "London" 
}, 
{ 
id: 4, 
name: "David Brown", 
email: "david.brown@example.com", address: "321 Elm Street", 
phone: "444-555-6666", 
country: "Australia", 
city: "Sydney" 
}, 
{ 
id: 5, 
name: "Emily Davis", 
email: "emily.davis@example.com", address: "654 Spruce Lane", 
phone: "333-444-5555", 
country: "USA", 
city: "Los Angeles" 
} 
]
,
            modalBootstrapInstance: null,
            autoSeleccionado: null,
            indiceSeleccionado: 0,
            names: [
                'Nombre',
                'Correo Electrónico' 
            ],
            marcaSeleccionado: "",
            modeloAbuscar:"",
            modalMode:"crear"
        }
    },
    components: {
        // Registro de componentes que se utilizaran.
        ContactoEditar,
        NuevoContactoView,
    },
    mounted() {
        this.$nextTick(() => {
            if (this.$refs.modalRef) {
                this.modalBootstrapInstance = new bootstrap.Modal(this.$refs.modalRef);
            } else {
                console.error('No se encontró el ref modalRef');
            }
        });
    },
    methods: {
        // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
        goToNew() {
            this.modalMode="crear";
            if (this.modalBootstrapInstance) {
                this.modalBootstrapInstance.show();
                
            } else {
                console.error('modalBootstrapInstance no está inicializado');
            }
        },
        abrirModal(index) {
            this.autoSeleccionado = null;
            this.indiceSeleccionado = index;
            this.modalMode="editar";
            setTimeout(() => {
                if (this.modalBootstrapInstance) {
                    this.modalBootstrapInstance.show();
                    this.autoSeleccionado = { ...this.items[index] };
                } else {
                    console.error('modalBootstrapInstance no está inicializado');
                }
            });

        },
        cerrarModal() {
            if (this.modalBootstrapInstance) {

                this.modalBootstrapInstance.hide();
            }
        },
        guardarEdicion(autoEditado) {
            console.log('Contacto editado:', autoEditado);
            // Aquí actualizas la info, haces llamada a API, etc.
            this.items[this.indiceSeleccionado] = autoEditado;
            this.cerrarModal();
        },

        eliminar(index) {
            if (confirm('¿Está seguro de eliminar este Contacto?')) {
                this.items.splice(index, 1);
            }
        },
        agregarNuevo($event){
            const maxId = Math.max(...this.items.map(auto => auto.id));
            $event['id'] = maxId + 1;
            this.items.push($event);
            console.log($event);
            this.cerrarModal();
        }

    },
    computed: {
        // propiedades computadas que dependen de otras propiedades reactivas
        getItems() {
            let result = [...this.items];
            
            if(this.anioAbuscar !== ""){
                result = result.filter((item) => { 
                    if(this.marcaSeleccionado == ""){
                        const _name = item.name || "";
                        const _email = item.email || "";
                        const _textToSearch = this.modeloAbuscar || "";
                        return _name.toLowerCase().includes(_textToSearch.toLocaleLowerCase()) || _email.toLowerCase().includes(_textToSearch.toLocaleLowerCase()); 
                    }else if(this.marcaSeleccionado == "Nombre"){
                        const _name = item.name || "";
                        const _textToSearch = this.modeloAbuscar || "";
                        return _name.toLowerCase().includes(_textToSearch.toLocaleLowerCase()); 
                    }else if(this.marcaSeleccionado == "Correo Electrónico"){
                        const _email = item.email || "";
                        const _textToSearch = this.modeloAbuscar || "";
                        return _email.toLowerCase().includes(_textToSearch.toLocaleLowerCase()); 
                    }  
                });
            }else{
                return result;      
            }

            return result;
        }
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script>

<style></style>