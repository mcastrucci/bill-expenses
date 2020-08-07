<template>
  <table class="table">
    <thead class="bg-blue text-white">
      <tr>
        <th scope="col">Date</th>
        <th scope="col">Amount</th>
        <th scope="col">Category</th>
        <th scope="col"></th>
      </tr>
    </thead>
    <tbody>
      <tr class="p-4 bg-blue-lighter text-center">
        <td colspan="4"><button class="underline" @click="triggerShowAddBill">Add new</button></td>
      </tr>
      <tr v-for="(bill, index) in bills" :key="index" class="p-4">
        <td>{{bill.date | moment("MMM D YYYY")}}</td>
        <td>${{bill.amount}}</td>
        <td>{{bill.category}}</td>
        <td><button @click="removeBill(index)">𝗫</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>

	export default {
		name: 'BillTable',
		components: {
			//whatever component you import
		},
		props: {
			bills: Array
		},
        methods: {
            triggerShowAddBill: function() {
                this.$emit('triggerShowAddBill')
            },
            removeBill: function(index) {
                this.$emit('removeBill', index)
            }
        }
	}
</script>

<style>
	
</style>