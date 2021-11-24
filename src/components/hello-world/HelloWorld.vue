<template>
  <div class="hello">
    <h2 class="text-center">{{ msg }}</h2>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">LastName</th>
          <th scope="col">FirstName</th>
          <th scope="col">SecondName</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="l in list" :key="l.lastName">
          <td>{{l.lastName}}</td>
          <td>{{l.firstName}}</td>
          <td>{{l.secondName}}</td>
        </tr>
      </tbody>
    </table>
    <paging :totalCount="totalCount" @change="setData" />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import Paging from '@/components/paging/paging.vue'
import { getTestData } from './helpers'
import { UserDto } from './user-dto'
@Component({
  components: {
    Paging
  }
})
export default class HelloWorld extends Vue {
  @Prop() private msg!: string

  totalCount: number = 0
  allList: UserDto[] = []
  list: UserDto[] = []

  mounted (): void {
    this.allList = getTestData()
    this.totalCount = this.allList.length
    this.setData()
  }

  setData (skipCount: number = 0, takeCount: number = 20): void {
    this.list = this.allList.slice().splice(skipCount, takeCount)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
