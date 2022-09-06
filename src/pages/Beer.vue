<template>
  <v-container>
    <v-row>
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Beer List Page
        </h1>
        <h3 class="font-weight-light">
          From Punk API
        </h3>
      </v-col>

      <v-col
        class="mb-5"
        cols="12"
      >
        <v-table>
          <thead>
            <tr>
              <th class="text-left">
                #
              </th>
              <th class="text-left">
                Name
              </th>
              <th class="text-left">
                Tagline
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="item in data"
              :key="item.name"
            >
              <td>{{ item.id }}</td>
              <td>{{ item.name }}</td>
              <td>{{ item.tagline }}</td>
            </tr>
          </tbody>
        </v-table>
        <div class="text-center ">
          <v-pagination
            v-model="page"
            :length="paginationLength"
            @change="getDataFromApi"
          ></v-pagination>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  const baseUrl = process.env.VUE_APP_API_BASEURL;
  const token = process.env.VUE_APP_API_TOKEN;

  import axios from "axios";

  export default {
    name: 'BeerList',

    data() {
      return {
        data: [],
        page: 1,
        perPage: 6,
        paginationLength: 6
      }
    },

    methods: {
      getDataFromApi() {
        axios.get(`${baseUrl}beers?page=${this.page}&per_page=${this.perPage}`,{
          headers: {
            'Accept': 'application/json',
            'Authorization': `Bearer ${token}` 
        }})
        .then(response => {
          this.data = response.data
        })
      },
   },

   watch: {
      page() {
        this.getDataFromApi()

        if(this.page == this.paginationLength) {
          this.paginationLength = this.paginationLength+3;
        }

        if(this.paginationLength-this.page>3) {
          this.paginationLength = this.paginationLength-3;
        }
      }
    },

    mounted() {
      this.getDataFromApi()
    },
  }
</script>
