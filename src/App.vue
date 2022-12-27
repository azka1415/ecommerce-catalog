<template>
	<div class="bg-pattern-error"></div>
	<div
		v-if="product"
		:class="
			product.category === 'women\'s clothing'
				? 'bg-pattern-pink'
				: product.category === 'jewelery'
				? 'bg-pattern-gold'
				: product.category === 'electronics'
				? 'bg-pattern-lightgray'
				: 'bg-pattern-blue'
		"
	></div>
	<div v-if="loading">
		<div class="home-loader">
			<HomeLoading />
		</div>
	</div>
	<div class="App">
		<ProductDisplay
			v-if="product"
			:product="product"
			:product-number="productNumber"
			:loading="loading"
			@nextProduct="setLoadingAndNextProduct(true)"
		/>
		<ProductError
			v-if="error"
			@resetProduct="setResetProduct()"
		/>
	</div>
</template>

<script>
import { ref, watchEffect } from "vue";
import "./assets/css/page.css";
import ProductDisplay from "./components/ProductDisplay.vue";
import HomeLoading from "./components/ProductLoading.vue";
import ProductError from "./components/ProductError.vue";

const product = ref(undefined);
const loading = ref(false);
const productNumber = ref(1);
const error = ref(false);
const setLoadingAndNextProduct = (value) => {
	productNumber.value += 1;
	loading.value = value;
};
const setResetProduct = () => {
	productNumber.value = 1;
	loading.value = true;
	error.value = false;
};

export default {
	setup() {
		loading.value = true;
		watchEffect(() => {
			fetch(`https://fakestoreapi.com/products/${productNumber.value}`)
				.then((res) => res.json())
				.catch((err) => {
					error.value = true;
					loading.value = false;
					console.log(err);
				})
				.then((data) => {
					product.value = data;
					loading.value = false;
				});
		});
	},
	data() {
		return {
			product,
			loading,
			productNumber,
			setLoadingAndNextProduct,
			error,
			setResetProduct,
		};
	},
	name: "App",
	components: {
		ProductDisplay,
		HomeLoading,
		ProductError,
	},
};
</script>
