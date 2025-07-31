<template>
  <div class="p-6 bg-gray-100 min-h-screen">
    <h1 class="text-2xl font-bold mb-6">Quadro de Horários</h1>

    <!-- Área de Quadros Adicionais -->
    <section class="mb-8">
      <h2 class="text-lg font-semibold mb-2">Quadros Adicionais</h2>
      <draggable
        v-model="adicionais"
        group="quadros"
        item-key="id"
        class="flex gap-4 flex-wrap bg-white p-4 rounded shadow"
      >
        <template #item="{ element }">
          <div class="bg-blue-100 p-4 rounded shadow w-48">
            {{ element.titulo }}
          </div>
        </template>
      </draggable>
    </section>

    <!-- Dias da Semana -->
    <section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <div
        v-for="(dia, index) in diasSemana"
        :key="index"
        class="bg-white p-4 rounded shadow"
      >
        <h3 class="font-semibold mb-2">{{ dia.nome }}</h3>
        <draggable
          v-model="dia.quadros"
          group="quadros"
          :disabled="dia.quadros.length >= 2"
          item-key="id"
          class="min-h-[100px] flex flex-col gap-2"
        >
          <template #item="{ element }">
            <div class="bg-green-100 p-4 rounded shadow">
              {{ element.titulo }}
            </div>
          </template>
        </draggable>
        <p v-if="dia.quadros.length >= 2" class="text-sm text-red-500 mt-2">
          Limite de 2 quadros atingido
        </p>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import draggable from 'vuedraggable'

const adicionais = ref([
  { id: 1, titulo: 'Quadro A' },
  { id: 2, titulo: 'Quadro B' },
  { id: 3, titulo: 'Quadro C' },
  { id: 4, titulo: 'Quadro D' },
])

const diasSemana = ref([
  { nome: 'Segunda', quadros: [] },
  { nome: 'Terça', quadros: [] },
  { nome: 'Quarta', quadros: [] },
  { nome: 'Quinta', quadros: [] },
  { nome: 'Sexta', quadros: [] },
  { nome: 'Sábado', quadros: [] },
])
</script>

<style scoped>
/* Tailwind*/
</style>
