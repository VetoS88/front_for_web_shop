<template>
  <q-page>
    <q-card>
      <q-card-section>
        <q-table
          grid
          title="Все товары"
          :rows="rows"
          :columns="columns"
          row-key="name"
          :filter="filter"
          hide-header
          no-data-label="Нет данных для отображения"
        >
          <template v-slot:top-right>
            <q-input outlined dense debounce="300" v-model="filter" placeholder="Поиск">
              <template v-slot:append>
                <q-icon name="search"/>
              </template>
            </q-input>
          </template>
        </q-table>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: "AllProductsListPage",
  data: () => ({
    rows: [

    ],
    columns: [],
    filter: ''
  }),

}
</script>

<style scoped>

</style>
