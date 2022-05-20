<template>
  <div class="container m-auto">
       <div class="rounded border m-2">
      <h1 class="p-2 text-4xl font-semi-bold text-gray-800">
        Nuxt.js Querying a GraphQL API
      </h1>
    </div>
     <div class="container mx-auto">
            <div class="flex flex-col">
                <div class="w-full">
                    <div class="p-4 border-b border-gray-200 shadow">
                        <!-- <table> -->
                        <table id="dataTable" class="p-4 w-full">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th class="p-8 text-xs text-gray-500">
                                        ID
                                    </th>
                                    <th class="p-8 text-xs text-gray-500">
                                        Name
                                    </th>
                                    <th class="p-8 text-xs text-gray-500">
                                        Email
                                    </th>
                                </tr>
                            </thead>
                            <tbody class="bg-white">
                                <tr class="whitespace-nowrap" v-for="data in hazura_hajura_table?hazura_hajura_table.slice((page - 1) * 10, page * 10):[]" :key="data.id">
                                    <td class="px-6 py-4 text-sm text-center text-gray-500">
                                      {{data.id}}
                                    </td>
                                    <td class="px-6 py-4 text-center">
                                        <div class="text-sm text-gray-900">
                                            {{data.name}}
                                        </div>
                                    </td>
                                    <td class="px-6 py-4 text-center">
                                        <div class="text-sm text-gray-500">{{data.email}}</div>
                                    </td>
                                </tr>

                            </tbody>
                        </table>
                         <Pagination
                            :page="page"
                            :totalPages="
                              hazura_hajura_table
                                ? Array(Math.ceil(hazura_hajura_table.length / 10))
                                    .fill(0)
                                    .map((e, i) => i + 1)
                                : []
                            "
                            :name="'users'"
                            :count="hazura_hajura_table ? hazura_hajura_table.length : 0"
                            :incrementpage="incrementpage"
                            :decrementpage="decrementpage"
                            :setpage="setpage"
                            :perpage="10"
                          />
                    </div>
                </div>
            </div>
        </div>
 
  </div>
</template>

<script>
import gql from 'graphql-tag'
import Pagination from '../components/Pagination.vue'
export default {
  components:{
    Pagination
  },
  data(){
    return{
      page:1
    }
  },
  methods:{
    incrementpage() {
      this.page = this.page + 1;
    },
    //go to previous oage
    decrementpage() {
      this.page = this.page - 1;
    },
    //go to perticular page
    setpage(page) {
      this.page = page;
    },
  },
  apollo: {
    hazura_hajura_table: gql`
      query MyQuery {
        hazura_hajura_table {
          id,
          name,
          email
        }
      }
    `,
  },
}
</script>

<style>
.main-pagination .pagination {display: flex;justify-content: center;}

.main-pagination .pagination button {width: 35px;height: 35px;border: 2px solid #000;line-height: 30px;margin: 0 10px;}

.main-pagination .pagination button.page-link-active {background: #000;color: #fff;}
</style>