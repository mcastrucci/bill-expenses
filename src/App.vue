<template>
  <main>
    <AddCategory v-if="shouldShowCategories" v-on:addCategory="addCategory"/>
    <div v-else>
      <AddBill v-if="shouldShowAddBill" :categories=categories v-on:addBill="addBill"/>
      <div v-else>
        <NavBar :categories=categories 
            v-on:triggerShowAddCategory="shouldShowCategories=true" 
            v-on:clearActiveCategory="clearActiveCategory" 
            v-on:setActiveCategory="setActiveCategory" />

        <div class="container flex">
          <div class="w-1/2">
            <BillsTable :bills="activeBills" v-on:triggerShowAddBill="shouldShowAddBill=true" v-on:removeBill="removeBill" />
          </div>
          <div class="w-1/2">
            <Chart :bills="activeBills" :activeCategory="activeCategory" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import AddBill from './components/AddBill';
import AddCategory from './components/AddCategory';
import BillsTable from './components/BillsTable';
import Chart from './components/Chart';
import NavBar from './components/NavBar';
import Vue from 'vue'

Vue.use(require('vue-moment'))


export default {
  name: 'App',
  components: {
    AddBill,
    AddCategory,
    BillsTable,
    Chart,
    NavBar
  },
  watch: {
    categories() {
      localStorage.setItem('categories', JSON.stringify(this.categories))
    },
    bills() {
      localStorage.setItem('bills', JSON.stringify(this.bills))
    },
  },
  mounted() {
    if (localStorage.getItem('categories')) {
      this.categories = JSON.parse(localStorage.getItem('categories'))
    }

    if (localStorage.getItem('bills')) {
      this.bills = JSON.parse(localStorage.getItem('bills'))
    }

    if (!this.categories.length) {
      this.shouldShowCategories = true
    } else {
      this.shouldShowAddBill = false;
    }
  },
  data: function () {
    return {
      bills: [],
      categories: [],
      shouldShowCategories: false,
      shouldShowAddBill: true,
      activeCategory: ''
    }
  },
  methods: {
    addCategory(category) {
      this.categories.push(category);
      this.shouldShowCategories = false;
    },
    addBill(bill) {
      this.bills.push(bill)
      this.shouldShowAddBill = false
    },
    removeBill(index) {
      this.bills.splice(index, 1);
    },
    clearActiveCategory() {
     this.activeCategory = ''
    },
    setActiveCategory(category) {
      this.activeCategory = category
    }
  },
  computed: {
    activeBills() {
      return this.bills
        .filter(
          bill =>
            this.activeCategory ? bill.category === this.activeCategory : true
        )
        .sort((a, b) => (new Date(a.date) < new Date(b.date) ? 1 : -1))
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
