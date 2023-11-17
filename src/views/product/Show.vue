<template>
	<div v-if="product === null">Loading...</div>
	<div v-else>
		<main>
			<!--Start Shop Details Breadcrumb-->
			<div class="shop-details-breadcrumb overflow-hidden">
				<div class="container">
					<div class="row">
						<div class="col-xl-12">
							<div class="shop-details-inner">
								<ul class="shop-details-menu">
									<li><a href="index.html">Home</a></li>
									<li class="active">Shop details</li>
								</ul>
							</div>
						</div>
					</div>
				</div>
			</div>
			<!--End Shop Details Breadcrumb-->
			<!--Start Shop Details Top-->
			<section class="shop-details-top two">
				<div class="container">
					<div class="row mt--30">
						<div class="col-xl-6 col-lg-6 mt-30">
							<div class="single-product-box one">
								<div class="big-product single-product-one slider-for">
									<div>
										<div class="single-item">
											<img :src="product.images[0].file_path" alt="">
										</div>
									</div>
								</div>
							</div>
						</div>
						<div class="col-xl-6 col-lg-6 mt-30">
							<div class="shop-details-top-right">
								<div class="shop-details-top-right-content-box">
									<div class="shop-details-top-title">
										<h3>{{ product.title }}</h3>
									</div>
									<!--<ul class="shop-details-top-info">
										<li><span>SKU:</span> {{ product.count }}</li>
									</ul>-->
									<div class="shop-details-top-price-box">
										<h3>
											{{ product.price }} $
											<del v-if="product.price_old">{{ product.price_old }} $</del>
										</h3>
									</div>
									<!--<div class="shop-details-top-size-box">
										<h4>Size</h4>
										<div class="shop-details-top-size-list-box">
											<ul class="shop-details-top-size-list">
												<li><a href="javascript:void(0);">XS</a></li>
												<li><a href="javascript:void(0);">S</a></li>
												<li><a href="javascript:void(0);">M</a></li>
												<li><a href="javascript:void(0);">XL</a></li>
											</ul>
										</div>
									</div>-->
									<div class="shop-details-top-color-sky-box">
										<h4>Color</h4>
										<ul class="varients">
											<li> <a href="javascript:void(0);" class="shop-details-top-color-sky-img"
											        data-src="/src/assets/images/shop/products-img1.jpg"> <img
												src="/src/assets/images/shop/shop-details-top-color-sky-img-1.jpg"
												alt=""> </a> </li>
											<li> <a href="javascript:void(0);" class="shop-details-top-color-sky-img"
											        data-src="/src/assets/images/shop/products-img2.jpg"> <img
												src="/src/assets/images/shop/shop-details-top-color-sky-img-2.jpg"
												alt=""> </a> </li>
											<li> <a href="javascript:void(0);" class="shop-details-top-color-sky-img"
											        data-src="/src/assets/images/shop/products-img3.jpg"> <img
												src="/src/assets/images/shop/shop-details-top-color-sky-img-3.jpg"
												alt=""> </a> </li>
											<li> <a href="javascript:void(0);" class="shop-details-top-color-sky-img"
											        data-src="/src/assets/images/shop/products-img4.jpg"> <img
												src="/src/assets/images/shop/shop-details-top-color-sky-img-4.jpg"
												alt=""> </a> </li>
										</ul>
									</div>
									<div class="product-quantity">
										<h4>Quantity</h4>
										<div class="product-quantity-box d-flex align-items-center flex-wrap">
											<div class="qty mr-2">
												<div class="qtySelector text-center">
													<span @click.prevent="decreaseQty" class="decreaseQty">
														<i class="flaticon-minus"></i>
													</span>
													<input type="number" id="qtyValue" value="1" readonly />
													<span @click.prevent="increaseQty" class="increaseQty">
														<i class="flaticon-plus"></i>
													</span>
												</div>
											</div>
											<!--<div class="product-quantity-check">
												<i class="flaticon-select"></i>
												<p>In stock</p>
											</div>-->
										</div>
									</div>
									<div class="shop-details-top-cart-box-btn pt-4">
										<button class="btn--primary style2" type="submit">Add to cart</button>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</section>
		</main>
	</div>
</template>

<script>
export default {
	name: 'Show',
	mounted() {
		$(document).trigger('changed');
		this.getProduct();
	},
	data() {
		return {
			product: null
		}
	},
	methods: {
		decreaseQty() {
			let newQty = Number($('#qtyValue').val()) - 1;

			if (newQty > 0) {
				$('#qtyValue').val(newQty);
			}
		},
		increaseQty() {
			let newQty = Number($('#qtyValue').val()) + 1;

			if (newQty < 100) {
				$('#qtyValue').val(newQty);
			}
		},
		getProduct() {
			this.axios.get(`http://ecommerce_shop.local/api/products/${this.$route.params.id}`)
				.then(res => {
					this.product = res.data.data;
					console.log(res);
				});
		}
	}
}
</script>
