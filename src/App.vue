<script setup>
    import { ref, reactive, onMounted } from "vue";
    import { db } from "./data/guitarras";
    import Guitarra from './components/guitarra.vue'
    import Header from "./components/header.vue";
    import Footer from "./components/footer.vue";
    
    const guitarras = ref([])
    const carrito = ref([]) 

    onMounted(() =>{
        guitarras.value = db;
    })
    
    const AgregarCarrito = (guitarra) =>{
        const ExisteCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)
        if (ExisteCarrito >= 0) {
            carrito.value[ExisteCarrito].cantidad++
        }else{
        guitarra.cantidad = 1;
        carrito.value.push(guitarra);
        }
    }

    const DecrementarCantidad = (() =>{
        console.log('cecrementar...');
        
    })

    const IncrementarCantidad = (() => {
        console.log('Incrementar...');
        
    })
</script>

<template>

    <Header 
    :carrito="carrito"
    @Decrementar-cantidad = "DecrementarCantidad"
    @Incrementar-cantidad = "IncrementarCantidad"
    />

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>
        <div class="row mt-5">

            <Guitarra 
            v-for="guitarra in guitarras"
            :guitarra="guitarra"
            @Agregar-Carrito="AgregarCarrito"
            />

        </div>
    </main>

    <Footer />

</template>



