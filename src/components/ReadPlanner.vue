<template>
  <div>
    <v-container>
      <v-row>
        <v-col cols="12" class="mx-auto">
          <h1 class="d-flex justify-center">Read planner</h1>
        </v-col>
      </v-row>
      <v-row class="d-print-none">
        <v-col cols="12" md="5">
          <v-text-field label="Total number of pages" type="number" v-model="pageCount"/>

        </v-col>
        <v-col cols="12" md="5">
          <v-text-field label="Total moments (days, weeks, months)" type="number"
                        v-model="momentCount"/>
        </v-col>
        <v-col cols="12" md="2">
          <v-btn @click="reset()" class="primary">reset</v-btn>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12">
          <v-simple-table v-if="pageCount * momentCount > 0">
            <template v-slot:default>
              <thead>
              <tr>
                <th>moment</th>
                <th>page</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="moment in readingTable" v-bind:key="moment.number">
                <td>{{ moment.number }}</td>
                <td>{{ moment.page }}</td>
              </tr>
              </tbody>
            </template>
          </v-simple-table>

        </v-col>
      </v-row>

    </v-container>
  </div>
</template>

<script>
export default {
  name: "read-planner",
  data() {
    return {
      pageCount: 0,
      momentCount: 0,
    }
  },
  methods: {
    reset() {
      this.pageCount = 0;
      this.momentCount = 0;
    }
  },
  computed: {
    readingTable() {
      const pagesPerMoment = Math.ceil(this.pageCount / this.momentCount);
      let table = [];
      let subTotalPages = 0;
      for (let i = 0; i < this.momentCount; i++) {
        subTotalPages += pagesPerMoment
        table.push({"number": i + 1, "page": Math.min(subTotalPages, this.pageCount)});
      }
      return table;
    }
  }
}
</script>