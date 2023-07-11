<script setup>
    import {ref} from 'vue';

    let teacher = ref({
        teacherName : '',
        teacherSurename : '',
        dni: '',
        subjects : [],
        docs : false
    });

    let teachers = ref([]);

    let subject = ref('');
</script>

<template>
    <section>
        <h3>Añadir profesor</h3>
        <div>
            <label>Nombre: </label>
            <input type="text" v-model="teacher.teacherName">
        </div>
        <div>
            <label>Apellidos: </label>
            <input type="text" v-model="teacher.teacherSurename">
        </div>
        <div>
            <label>DNI: </label>
            <input type="text" v-model="teacher.dni">
        </div>
        <div>
            <label>Materias: </label>
            <input type="text" v-model="subject">
            <button>Agregar</button>
        </div>
        <input type="checkbox" v-model="teacher.docs"> Documentación entregada
        <button>Enviar</button> 
    </section>
    <section>
        <h3>Listado de profesores: </h3>
    </section>
</template>

<style scoped>

</style>