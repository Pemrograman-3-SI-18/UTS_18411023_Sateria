<template>
  <q-page class="bg-blue-grey" view="hHh Lpr LFf">
    <div class="q-pa-md">
      <q-table
        title="Treats"
        :data="data"
        :columns="columns"
        row-key="id"
        :filter="filter"
        :loading="loading"
      >

        <template v-slot:top>
          <q-btn color="blue" :disable="loading" label="Tambah Data Topi" to="/admin/inputdata" />
          <!-- <q-btn class="q-ml-sm" color="primary" :disable="loading" label="Remove row" @click="removeRow" /> -->
          <q-space />
          <q-input borderless dense debounce="300" color="primary" v-model="filter">
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </template>

      </q-table>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      filter: '',
      rowCount: 10,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Kode Topi',
          align: 'left',
          field: row => row.kode,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'model', align: 'center', label: 'Model Topi', field: 'model', sortable: true },
        { name: 'stok', align: 'center', label: 'Jumlah Stok', field: 'stok', sortable: true },
        { name: 'harga', align: 'center', label: 'Harga Sepeda', field: 'harga' }
      ],

      data: [
        {
          kode: 'TOP001',
          model: 'Topi Korea Bola Fashion Trend Kasual Logam',
          stok: '100',
          harga: 'Rp.52.000'
        },

        {
          kode: 'TOP002',
          model: 'Topi Beret Desain BTS Kim Tae Hung',
          stok: '56',
          harga: 'Rp.60.000'
        },

        {
          kode: 'TOP003',
          model: 'Topi Beret Casual Bahan Octagonal Hangat',
          stok: '95',
          harga: 'RP.50.000'
        },

        {
          kode: 'TOP004',
          model: 'Topi koboy koboi zorro fedora pita original',
          stok: '35',
          harga: 'Rp.35.000'
        },

        {
          kode: 'TOP005',
          model: 'Topi Datar Luar Ruangan Yang Hangat Aksesori',
          stok: '10',
          harga: 'Rp45.000'
        },

        {
          kode: 'TOP006',
          model: 'Topi Bucket Bahan Corduroy Bordir Tulisan',
          stok: '44',
          harga: 'Rp.60.000'
        }
      ]
    }
  },

  methods: {
    // emulate fetching data from server
    addRow () {
      this.loading = true
      setTimeout(() => {
        const
          index = Math.floor(Math.random() * (this.data.length + 1)),
          row = this.original[Math.floor(Math.random() * this.original.length)]
        if (this.data.length === 0) {
          this.rowCount = 0
        }
        row.id = ++this.rowCount
        const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
        this.data = [...this.data.slice(0, index), addRow, ...this.data.slice(index)]
        this.loading = false
      }, 500)
    },

    removeRow () {
      this.loading = true
      setTimeout(() => {
        const index = Math.floor(Math.random() * this.data.length)
        this.data = [...this.data.slice(0, index), ...this.data.slice(index + 1)]
        this.loading = false
      }, 500)
    }
  }
}
</script>
