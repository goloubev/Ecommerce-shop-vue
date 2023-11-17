<template>
	<div v-if="products === null">Loading...</div>
	<div v-else>
		<main class="overflow-hidden">
			<section class="cart-area pt-120 pb-120">
				<div class="container">
					<div v-if="products.length > 0">
						<div class="row">
							<div class="col-xl-12 col-lg-12 col-md-12 col-sm-12">
								<div class="cart-table-box">
									<div class="table-outer">
										<table class="cart-table">
											<thead class="cart-header">
												<tr>
													<th class="">Product</th>
													<th class="price">Price</th>
													<th>Qty</th>
													<th>Subtotal</th>
													<th class="hide-me"></th>
												</tr>
											</thead>
											<tbody>
												<tr v-for="product in products">
													<td>
														<div class="thumb-box">
															<router-link :to="{ name: 'products.show', params: { id: product.id }}" class="thumb">
																<img :src="product.image_url" :alt="product.title" />
															</router-link>
															<router-link :to="{ name: 'products.show', params: { id: product.id }}" class="title">
																<h5>{{ product.title }}</h5>
															</router-link>
														</div>
													</td>
													<td>{{ product.price }} $</td>
													<td class="qty">
														<div class="qtySelector text-center">
															<span @click.prevent="decreaseQty(product)" class="decreaseQty">
																<i class="flaticon-minus"></i>
															</span>
															<input type="number" class="qtyValue" :value="product.qty" readonly />
															<span @click.prevent="increaseQty(product)" class="increaseQty">
																<i class="flaticon-plus"></i>
															</span>
														</div>
													</td>
													<td class="sub-total">{{ (product.price * product.qty).toFixed(2) }} $</td>
													<td>
														<div @click.prevent="removeProduct(product.id)" class="remove">
															<i class="flaticon-cross"></i>
														</div>
													</td>
												</tr>
											</tbody>
										</table>
									</div>
								</div>
							</div>
						</div>
						<div class="row w-25 pt-4">
							<div class="col-xl-12">
								<input type="text" v-model="name" placeholder="Name">
								<input type="text" v-model="email" placeholder="Email">
								<input type="text" v-model="address" placeholder="Address">
								<p>&nbsp;</p>
								<input @click.prevent="storeOrder()" type="submit" class="btn btn-primary" value="SUBMIT" />
							</div>
						</div>
						<div class="row pt-120">
							<div class="col-xl-6 col-lg-7">
								<h3>Cart total: <span id="total_price">{{ total_price }}</span> $</h3>
							</div>
						</div>
					</div>
					<div v-else>
						No products in your cart
					</div>
				</div>
			</section>
		</main>
	</div>
</template>

<script>
export default {
	name: 'Index',
	mounted() {
		$(document).trigger('changed');
		this.getCartProducts();
		this.totalPrice();
	},
	data() {
		return {
			name: '',
			email: '',
			address: '',
			products: [],
			total_price: 0,
		}
	},
	methods: {
		decreaseQty(product) {
			let newQty = product.qty - 1;

			if (newQty > 0) {
				product.qty--;
				this.updateCart();
			}
		},
		increaseQty(product) {
			let newQty = product.qty + 1;

			if (newQty < 100) {
				product.qty++;
				this.updateCart();
			}
		},
		removeProduct(product_id) {
			this.products = this.products.filter(product => {
				return product.id != product_id;
			});
			this.updateCart();
		},
		updateCart() {
			localStorage.setItem('cart', JSON.stringify(this.products));
			this.totalPrice();
		},
		totalPrice() {
			let total = 0;

			this.products.forEach(product => {
				total = total + (Number(product.price) * product.qty);
			});
			this.total_price = total.toFixed(2);
		},
		getCartProducts() {
			this.products = JSON.parse(localStorage.getItem('cart'));
			//console.log(this.products);
		},
		storeOrder() {
			const data = {
				'name': this.name,
				'email': this.email,
				'address': this.address,
				'products': this.products,
				'total_price': this.total_price,
			};

			this.axios.post('http://ecommerce_shop.local/api/orders', data)
				.then(res => {
					if (res.statusText == "Created") {
						this.products.forEach(product => {
							this.removeProduct(product.id);
						});
					}
				});
		}
	}
}
</script>
