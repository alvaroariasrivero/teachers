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

    const handleSubject = () => {
        teacher.value.subjects.push(subject.value);
        subject.value = '';
    };

    const handleTeacher = () => {
        teachers.value.push({
            teacherName: teacher.value.teacherName,
            teacherSurename: teacher.value.teacherSurename,
            dni : teacher.value.dni,
            subjects: teacher.value.subjects,
            docs: teacher.value.docs
        });
        teacher.value.teacherName = '';
        teacher.value.teacherSurename = '';
        teacher.value.dni = '';
        teacher.value.subjects = [];
        teacher.value.docs = false;
    };

    const deleteTeacher = (index) => {
        teachers.value.splice(index, 1);
    };

    // const editTeacher = (index) => {
    //     let teachersArray = Array.from(teachers.value)
    //     console.log('flipándome', teachersArray[1]);
    // }


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
            <button @click="handleSubject()">Agregar</button>
        </div>
        <div>
            <ul>
                <li v-for="(elem, index) in teacher.subjects" v-bind:key="index">{{ elem }}</li>
            </ul>
        </div>
        <input type="checkbox" v-model="teacher.docs"> Documentación entregada
        <button @click="handleTeacher()">Enviar</button> 
    </section>
    <section>
        <h3>Listado de profesores: </h3>
        <table>
            <th>Nombre</th>
            <th>Apellidos</th>
            <th>DNI</th>
            <th>Materias</th>
            <th>Documentación</th>
            <tr v-for="(elm, index) in teachers" :key="index">
                <td>{{ elm.teacherName }}</td>
                <td>{{ elm.teacherSurename }}</td>
                <td>{{ elm.dni }}</td>
                <td>
                    <ul>
                        <li v-for="(item, index) in elm.subjects" :key="index">{{ item }}</li>
                    </ul>
                </td>
                <td v-if="elm.doc">Entregada</td>
                <td v-else>No entregada</td>
                <td><button @click="deleteTeacher(index)">Borrar</button></td>
                <td><button>Editar</button></td>
            </tr>
        </table>
    </section>
</template>

<style scoped>

</style>