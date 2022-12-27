<template>
	<LoadingProduct v-if="loading" />
	<div class="container">
		<div class="product-image">
			<img
				:src="product.image"
				alt="Product Image"
				class="product-image"
			/>
		</div>
		<div class="product-body">
			<div class="product-header">
				<h1
					:class="
						product.category === 'women\'s clothing'
							? 'text-color-purple'
							: product.category === 'jewelery'
							? 'text-color-gold'
							: 'text-color-blue'
					"
				>
					{{ product.title }}
				</h1>
				<div class="product-category">
					<span>{{ product.category }}</span>
					<div class="product-rating">
						<span>{{ product.rating.rate }}/5</span>
						<div
							v-if="product.category === 'women\'s clothing'"
							class="product-rating-circles"
						>
							<PurpleCircle
								v-for="(star, index) in Math.floor(product.rating.rate)"
								:key="index + star"
							/>
							<WhiteCircle
								v-for="(star, index) in 5 - Math.floor(product.rating.rate)"
								:key="index + star"
							/>
						</div>
						<div
							v-else-if="product.category === 'men\'s clothing'"
							class="product-rating-circles"
						>
							<BlueCircle
								v-for="(star, index) in Math.floor(product.rating.rate)"
								:key="index + star"
							/>
							<WhiteCircle
								v-for="(star, index) in 5 - Math.floor(product.rating.rate)"
								:key="index + star"
							/>
						</div>
						<div
							v-else-if="product.category === 'jewelery'"
							class="product-rating-circles"
						>
							<GoldCircle
								v-for="(star, index) in Math.floor(product.rating.rate)"
								:key="index + star"
							/>
							<WhiteCircle
								v-for="(star, index) in 5 - Math.floor(product.rating.rate)"
								:key="index + star"
							/>
						</div>
					</div>
				</div>
			</div>
			<div class="product-main">
				<p>
					{{ product.description }}
				</p>
			</div>
			<div class="product-footer">
				<h2
					:class="
						product.category === 'women\'s clothing'
							? 'text-color-purple'
							: product.category === 'jewelery'
							? 'text-color-gold'
							: 'text-color-blue'
					"
				>
					${{ product.price }}
				</h2>
				<div class="product-buttons">
					<div
						:class="
							product.category === 'women\'s clothing'
								? 'buy-btn buy-btn-purple'
								: product.category === 'jewelery'
								? 'buy-btn buy-btn-gold'
								: 'buy-btn buy-btn-blue'
						"
					>
						Buy now
					</div>
					<div
						:class="
							product.category === 'women\'s clothing'
								? 'next-btn next-btn-purple'
								: product.category === 'jewelery'
								? 'next-btn next-btn-gold'
								: 'next-btn next-btn-blue'
						"
						@click="nextProduct()"
					>
						Next product
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
import PurpleCircle from "./PurpleCircle.vue";
import WhiteCircle from "./WhiteCircle.vue";
import BlueCircle from "./BlueCircle.vue";
import GoldCircle from "./GoldCircle.vue";
import LoadingProduct from "./ProductLoading.vue";

export default {
	name: "ProductDisplay",
	components: {
		PurpleCircle,
		WhiteCircle,
		BlueCircle,
		LoadingProduct,
		GoldCircle,
	},
	props: {
		product: {
			type: Object,
			required: true,
		},
		productNumber: {
			type: Number,
			required: true,
		},
		loading: {
			type: Boolean,
			required: true,
		},
	},
	methods: {
		nextProduct() {
			this.$emit("nextProduct");
		},
	},
	emits: ["nextProduct"],

	data() {
		return {};
	},
};
</script>
