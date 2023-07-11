<script setup>
    import { ref } from 'vue';

    let teacher = ref({
        teacherName: '',
        teacherSurename: '',
        dni: '',
        subjects: [],
        docs: false,
    });

    let teachers = ref([]);

    let editedTeacher = ref(null); // Inicializamos con null para indicar que no se está editando ningún profesor actualmente

    let subject = ref('');

    const handleSubject = () => {
        teacher.value.subjects.push(subject.value);
        subject.value = '';
    };

    const handleTeacher = () => {
        if (editedTeacher.value === null) {
            // Agregar nuevo profesor
            teachers.value.push({
                teacherName: teacher.value.teacherName,
                teacherSurename: teacher.value.teacherSurename,
                dni: teacher.value.dni,
                subjects: teacher.value.subjects,
                docs: teacher.value.docs,
            });
        } else {
            // Actualizar profesor existente
            editedTeacher.value.teacherName = teacher.value.teacherName;
            editedTeacher.value.teacherSurename = teacher.value.teacherSurename;
            editedTeacher.value.dni = teacher.value.dni;
            editedTeacher.value.subjects = teacher.value.subjects;
            editedTeacher.value.docs = teacher.value.docs;
            editedTeacher.value = null; // Reiniciamos editedTeacher después de la actualización
        }
        teacher.value.teacherName = '';
        teacher.value.teacherSurename = '';
        teacher.value.dni = '';
        teacher.value.subjects = [];
        teacher.value.docs = false;
    };

    const deleteTeacher = (index) => {
        teachers.value.splice(index, 1);
    };

    const editTeacher = (index) => {
        editedTeacher.value = teachers.value[index];
        teacher.value = { ...teachers.value[index] };
    };
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
                <td>{{ index === editedTeacher ? teacher.teacherName : elm.teacherName }}</td>
                <td>{{ index === editedTeacher ? teacher.teacherSurename : elm.teacherSurename }}</td>
                <td>{{ index === editedTeacher ? teacher.dni : elm.dni }}</td>
                <td>
                    <ul>
                    <li v-for="(item, index) in (index === editedTeacher ? teacher.subjects : elm.subjects)" :key="index">{{ item }}</li>
                    </ul>
                </td>
                <td v-if="elm.docs">Entregada</td>
                <td v-else>No entregada</td>
                <td><button @click="deleteTeacher(index)">Borrar</button></td>
                <td><button @click="editTeacher(index)">Editar</button></td>
            </tr>
        </table>
    </section>
</template>

<style scoped>

</style>