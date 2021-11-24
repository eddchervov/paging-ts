
<template>
    <div>
        <div class="row">
            <div class="col-xl-6">
                <!-- Paging https://github.com/lokyoung/vuejs-paginate -->
                <template v-if="totalPage > 1">
                    <vue-paging v-model="currentPage"
                                  :page-count="totalPage"
                                  :page-range="5"
                                  :margin-pages="1"
                                  :click-handler="clickPaging"
                                  :prev-text="'Предыдущая'"
                                  :next-text="'Следующая'"
                                  :container-class="'pagination'"
                                  :page-link-class="'page-link'"
                                  :page-class="'page-item'"
                                  :prev-link-class="'page-link'"
                                  :prev-class="'page-item'"
                                  :next-link-class="'page-link'"
                                  :next-class="'page-item'">
                    </vue-paging>
                </template>
            </div>
            <div class="col-xl-6">
                <ul class="pagination float-md-end">
                    <li class="pt-1 me-3">Кол-во элементов на страницу: </li>
                    <li class="page-item"
                        v-bind:class="{ 'active': pageSize === 20 }"
                        v-on:click="changePageSize(20)">
                        <button class="page-link">
                            20
                        </button>
                    </li>
                    <li class="page-item"
                        v-bind:class="{ 'active': pageSize === 40 }"
                        v-on:click="changePageSize(40)">
                        <button class="page-link">
                            40
                        </button>
                    </li>
                    <li class="page-item"
                        v-bind:class="{ 'active': pageSize === 60 }"
                        v-on:click="changePageSize(60)">
                        <button class="page-link">
                            60
                        </button>
                    </li>
                </ul>
            </div>
        </div>
        <div class="row" v-if="totalPage > 1 && isMessage">
            <div class="col-xl-6 text-start">
                <span v-text="message"></span>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component({
  components: {
    VuePaging: require('vuejs-paginate')
  }
})
export default class Paging extends Vue {
  @Prop() readonly totalCount!: number
  @Prop({ type: Boolean, default: true }) readonly isMessage!: boolean
  pageSize: number = 20
  currentPage: number = 1

  get skipCount (): number {
    return (this.currentPage - 1) * this.pageSize
  }

  get takeCount (): number {
    return this.pageSize
  }

  get totalPage (): number {
    return Math.floor((this.totalCount + this.pageSize - 1) / this.pageSize)
  }

  get message (): string {
    if (this.totalPage === 0) return ''
    const from = (this.currentPage - 1) * this.pageSize + 1
    let to = from + this.pageSize - 1
    to = to >= this.totalCount ? this.totalCount : to

    return 'Показаны с ' + from + ' по ' + to + ' из ' + this.totalCount + ' записей'
  }

  clickPaging (e: number): void {
    this.currentPage = e
    this.reloadEntityTable()
  }

  reloadEntityTable (): void {
    this.$emit('change', this.skipCount, this.takeCount)
  }

  reloadAndGoFirstPageEntityTable (): void {
    this.currentPage = 1
    this.reloadEntityTable()
  }

  changePageSize (count: number): void {
    this.pageSize = count
    this.reloadAndGoFirstPageEntityTable()
  }
}
</script>
