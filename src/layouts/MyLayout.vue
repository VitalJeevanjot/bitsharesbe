<template>
<q-layout view="lHh Lpr lFf">
  <q-layout-header class="no-shadow">
    <q-toolbar :inverted="$q.theme === 'ios'" color="black">
      <q-toolbar-title class="text-white">
        <div align="center">
          BitsharesBE
        </div>
      </q-toolbar-title>
    </q-toolbar>
  </q-layout-header>
  <q-page-container>
    <q-page>
      <div class="row justify-center q-pa-sm">
        <div class=""> </div>
        <div class="col-8">
          <!-- <q-search icon="search" color="black" inverted clearable placeholder="Unit id" /> -->
        </div>
        <!-- <div class="q-pl-md">
          <q-btn color="black" size="md" icon="search" @click="loadData" />
        </div> -->
      </div>
      <q-list highlight class="full-width" v-for="item in items" :key="item.id">
        <q-list-header>{{item.id}}</q-list-header>
        <q-item>
          <a :href="'https://cryptofresh.com/a/' + item.coinID">{{item.coinID}}</a>
        </q-item>
      </q-list>
    </q-page>
  </q-page-container>
</q-layout>
</template>

<script>
export default {
  name: 'MyLayout',
  data () {
    return {
      items: []
    }
  },
  methods: {
    loadData: function () {
      this.$axios.get(`http://185.208.208.184:5000/assets`).then(response => {
        console.log(response.data)
        for (var i = 0; i < response.data.length; i++) {
          this.items.push({
            coinID: response.data[i][1],
            id: response.data[i][2]
          })
        }
      }).catch((e) => {
        // console.log(e)
      })
    }
  },
  mounted () {
    console.log('running')
    this.loadData()
  }
}
</script>

<style>
</style>
