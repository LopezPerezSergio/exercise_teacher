<template>
    <section>
        <h3>Añadir Profesor</h3>

        <div>
            <label for="">Nombre:</label>
            <input type="text" v-model="teacher.teacherName">
        </div>
        <div>
            <label for="">Apellidos:</label>
            <input type="text" v-model="teacher.surname">
        </div>
        <div>
            <label for="">DNI / NIF:</label>
            <input type="text" v-model="teacher.dni">
        </div>
        <div>
            <label for="">Materias:</label>
            <input type="text" v-model="subject"> <button @click="handleSubject()">Agregar</button>
        </div>
        <div>
            <ul>
                <li v-for="(subject, index) in teacher.subjects" :key="index">
                    {{ subject }}
                </li>
            </ul>
        </div>
        <input type="checkbox" v-model="teacher.doc"> Documentacion Entregada

        <button @click="handleTeacher()">Agregar</button>
    </section>

    <section>
        <h3>Listado de Profesores</h3>

        <table>
            <thead>
                <th>Nombre</th>
                <th>Apellidos</th>
                <th>DNI / NIF</th>
                <th>Materias</th>
                <th>Documentacion Entregada</th>
            </thead>
            <tbody>
                <tr v-for="teacher in teachers" :key="teacher.dni">
                    <th>{{ teacher.teacherName }}</th>
                    <th>{{ teacher.surname }}</th>
                    <th>{{ teacher.dni }}</th>
                    <th>
                        <ul>
                            <li v-for="(subject, index) in teacher.subjects" :key="index">
                                {{ subject }}
                            </li>
                        </ul>
                    </th>
                    <th v-if="teacher.doc">Entregado</th>
                    <th v-else>No entregado</th>
                </tr>
            </tbody>
        </table>
    </section>
</template>

<script lang="ts" setup>
import { Ref, ref } from 'vue'

interface ITeacher {
    teacherName: string,
    surname: string,
    dni: string,
    subjects: Array<string>,
    doc: boolean
}

let teacher: Ref<ITeacher> = ref({
    teacherName: '',
    surname: '',
    dni: '',
    subjects: [],
    doc: false
})

let teachers: Ref<Array<ITeacher>> = ref([])

let subject: Ref<string> = ref('')

const handleSubject = () => {
    teacher.value.subjects.push(subject.value)
    subject.value = ''
}

const handleTeacher = () => {
    teachers.value.push({
        teacherName: teacher.value.teacherName,
        surname: teacher.value.surname,
        dni: teacher.value.dni,
        subjects: teacher.value.subjects,
        doc: teacher.value.doc
    })

    teacher.value.teacherName = ''
    teacher.value.surname = ''
    teacher.value.dni = ''
    teacher.value.doc = false
    teacher.value.subjects = []
}
</script>

<style scoped></style>