<template>
  <ul class="list-reset inline flex justify-center border-b-4 mb-0">
    <li
        class="p-4 inline hover:bg-grey-light uppercase font-black cursor-pointer"
        :class="[ activeCategory === '' ? 'bg-grey-dark' : 'bg-grey-lighter' ]"
        @click="clearActiveCategory()">
        All
    </li>
    <li
    class="p-4 inline hover:bg-grey-light uppercase font-black cursor-pointer"
    :class="[ activeCategory === category ? 'bg-grey-dark' : 'bg-grey-lighter' ]"
    v-for="category in categories"
    :key="category"
    @click="setActiveCategory(category)" >
    {{category}}
    </li>

    <li class="p-4 inline bg-grey-lighter hover:bg-grey-light uppercase font-black cursor-pointer" @click="triggerShowAddCategory">➕</li>
  </ul>
</template>

<script>

	export default {
		name: 'NavBar',
		components: {
			//whatever component you import
		},
		props: {
			categories: Array,
            activeCategory: String
		},
        methods: {
            triggerShowAddCategory() {
                this.$emit('triggerShowAddCategory');
            },
            clearActiveCategory() {
                this.$emit('clearActiveCategory')
            },
            setActiveCategory(category) {
                this.$emit('setActiveCategory', category)
            }
        }
	}
</script>

<style>
	
</style>