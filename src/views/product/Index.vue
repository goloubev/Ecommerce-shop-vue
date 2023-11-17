<template>
	<div v-if="products === null || filterList === null">Loading...</div>
	<div v-else>
		<main class="overflow-hidden">
			<!--Start product-grid-->
			<div class="product-grid pt-60 pb-120">
				<div class="container">
					<div class="row gx-4">
						<div class="col-xl-3 col-lg-4">
							<div class="shop-grid-sidebar">
								<div class="sidebar-holder">
									<div v-if="filterList.categories" class="single-sidebar-box mt-30">
										<h4>Categories</h4>
										<div class="checkbox-item">
											<form>
												<div v-for="category in filterList.categories" class="form-group">
												<input type="checkbox" :value="category.id" :id="`category_${category.id}`" v-model="categories">
													<label :for="`category_${category.id}`">{{ category.title }}</label>
												</div>
											</form>
										</div>
									</div>
									<div v-if="filterList.colors" class="single-sidebar-box mt-30">
										<h4>Colors</h4>
										<ul class="color-option">
											<li v-for="color in filterList.colors">
												<a href="javascript:void(0);"
												   @click.prevent="addColor(color.id)"
												   :style="{background:color.title}"
												   class="color-option-single"
												   :class="{'border border-2 border-dark': colors.includes(color.id)}"
												>
													<span>{{ color.title }}</span>
												</a>
											</li>
										</ul>
									</div>
									<div v-if="filterList.tags" class="single-sidebar-box mt-30 pb-0 border-bottom-0">
										<h4>Tags</h4>
										<ul class="popular-tag">
											<li v-for="tag in filterList.tags">
												<a href="javascript:void(0);"
												   @click.prevent="addTag(tag.id)"
												   :class="{'border border-1 border-dark': tags.includes(tag.id)}"
												>
													{{ tag.title }}
												</a>
											</li>
										</ul>
									</div>
									<div v-if="filterList.price" class="single-sidebar-box mt-30">
										<h4>Prices</h4>
										Min: <input id="price_min" value="1" style="border: solid 1px lightgray; width: 90px;" maxlength="4" />
										Max: <input id="price_max" value="999" style="border: solid 1px lightgray; width: 90px;" maxlength="4" />
									</div>
									<div class="single-sidebar-box mt-30">
										<div class="slider-box">
											<button class="filterbtn" type="button" @click.prevent="filterClear()" style="border: solid 1px black; margin-right:10px;">Clear</button>
											<button class="filterbtn" type="submit" @click.prevent="filterProducts()" style="border: solid 1px black;">Filter</button>
										</div>
									</div>
								</div>
							</div>
						</div>
						<div class="col-xl-9 col-lg-8">
							<div class="row">
								<div class="col-xl-12">
									<div class="shop-grid-page-top-info p-0 justify-content-md-between justify-content-center">
										<div class="left-box">
											<p>Showing 1–12 of 50 results</p>
										</div>
										<div class="right-box justify-content-md-between justify-content-center">
											<div class="short-by">
												<div class="select-box">
													<form>
														<select id="order" style="border: solid 1px lightgray;" v-model="order" @change="addOrder($event)">
															<option value="title|asc">Alphabetically, A-Z</option>
															<option value="title|desc">Alphabetically, Z-A</option>
															<option value="price|asc">Price, low to high</option>
															<option value="price|desc">Price, high to low</option>
														</select>
													</form>
												</div>
											</div>
											<div class="product-view-style d-flex justify-content-md-between justify-content-center">
												<ul class="nav nav-pills" id="pills-tab" role="tablist">
													<li class="nav-item" role="presentation">
														<button class="nav-link active" id="pills-grid-tab"
														        data-bs-toggle="pill" data-bs-target="#pills-grid" type="button"
														        role="tab"  aria-selected="true">
															<i class="flaticon-grid"></i>
														</button>
													</li>
													<li class="nav-item" role="presentation">
														<button class="nav-link" id="pills-list-tab" data-bs-toggle="pill"
														        data-bs-target="#pills-list" type="button" role="tab"
														        aria-selected="false">
															<i class="flaticon-list"></i>
														</button>
													</li>
												</ul>
												<button class="slidebarfilter d-lg-none d-flex">
													<i class="flaticon-edit"></i>
												</button>
											</div>
										</div>
									</div>
								</div>
							</div>
							<div class="row">
								<div class="col-12">
									<div class="tab-content" id="pills-tabContent">
										<div class="tab-pane fade show active" id="pills-grid" role="tabpanel" aria-labelledby="pills-grid-tab">
											<div class="row">
												<div v-if="products.length > 0" v-for="product in products" class="col-xl-4 col-lg-6 col-6">
													<div class="products-three-single w-100 mt-30">
														<div class="products-three-single-img">
															<router-link :to="{ name: 'products.show', params: { id: product.id }}" class="d-block">
																<!-- :src !!!!! -->
																<img :src="product.images[0].file_path" alt="" />
															</router-link>
															<a @click.prevent="addToCart(product, true)" href="javascript:void(0);" class="addcart btn--primary style2">Add to cart</a>
															<div class="products-grid__usefull-links">
																<ul>
																	<li>
																		<a href="javascript:void(0);"><i class="flaticon-heart"></i>
																			<span>Wishlist</span>
																		</a>
																	</li>
																	<li>
																		<a href="javascript:void(0);">
																			<i class="flaticon-left-and-right-arrows"></i>
																			<span>Compare</span>
																		</a>
																	</li>
																	<li>
																		<a @click="getProduct(product.id)" :href="`#popup_${product.id}`" class="popup_link">
																			<i class="flaticon-visibility"></i>
																			<span>Quick view</span>
																		</a>
																	</li>
																</ul>
															</div>
														</div>
														<div :id="`popup_${product.id}`" class="product-gird__quick-view-popup mfp-hide">
															<div v-if="popupProduct" class="container">
																<div class="row justify-content-between align-items-center">
																	<div class="col-lg-6">
																		<div class="quick-view__left-content">
																			<div class="tabs">
																				<div class="popup-product-thumb-box">
																					<ul>
																						<li v-for="(image, index) in popupProduct.images" class="tab-nav popup-product-thumb">
																							<a :href="`#tabb_${index}`">
																								<img :src="image.file_path" alt="" />
																							</a>
																						</li>
																					</ul>
																				</div>
																				<div class="popup-product-main-image-box">
																					<div v-for="(image, index) in popupProduct.images" :id="`tabb_${index}`" class="tab-item popup-product-image">
																						<div class="popup-product-single-image">
																							<img :src="image.file_path" alt="" />
																						</div>
																					</div>
																					<button class="prev" v-if="popupProduct.images.length > 2">
																						<i class="flaticon-back"></i>
																					</button>
																					<button class="next" v-if="popupProduct.images.length > 2">
																						<i class="flaticon-next"></i>
																					</button>
																				</div>
																			</div>
																		</div>
																	</div>
																	<div class="col-lg-6">
																		<div class="popup-right-content">
																			<h3>{{ popupProduct.title }}</h3>
																			<p class="text">
																				{{ popupProduct.category.title }}
																			</p>
																			<p class="text">
																				{{ popupProduct.description }}
																			</p>
																			<div class="price">
																				<h2>
																					{{ popupProduct.price }} $
																					<del v-if="popupProduct.price_old">{{ popupProduct.price_old }} $</del>
																				</h2>
																			</div>
																				<div class="color-varient">
																					<template v-for="groupProduct in popupProduct.group_products">
																						<a @click.prevent="getProduct(groupProduct.id)" v-for="color in groupProduct.colors" :style="`background:${color.title};`" href="javascript:void(0);" class="color-name"></a>
																					</template>
																				</div>
																			<div class="add-product">
																				<h6>Qty:</h6>
																				<div class="button-group">
																					<div class="qtySelector text-center">
																						<span @click.prevent="decreaseQty" class="decreaseQty">
																							<i class="flaticon-minus"></i>
																						</span>
																						<input type="number" id="qtyValue" value="1" readonly />
																						<span @click.prevent="increaseQty" class="increaseQty">
																							<i class="flaticon-plus"></i>
																						</span>
																					</div>
																					<button @click.prevent="addToCart(popupProduct, false)" class="btn--primary">
																						Add to cart
																					</button>
																				</div>
																			</div>
																		</div>
																	</div>
																</div>
															</div>
														</div>
														<div class="products-three-single-content text-center">
															<span>{{ product.category.title }}</span>
															<h5>
																<router-link :to="{ name: 'products.show', params: { id: product.id }}">
																	{{ product.title }}
																</router-link>
															</h5>
															<p>
																<del v-if="product.price_old">{{ product.price_old }} $</del>
																{{ product.price }} $
															</p>
														</div>
													</div>
												</div>
											</div>
										</div>
									</div>
								</div>
							</div>
							<div class="row" v-if="pagination.last_page > 1">
								<div class="col-12 d-flex justify-content-center">
									<ul class="pagination text-center">
										<li>
											<a @click.prevent="getProducts(1)" href="javascript:void(0);">First</a>
										</li>
										<li v-if="pagination.current_page !== 1">
											<a @click.prevent="getProducts(pagination.current_page - 1)" href="javascript:void(0);">
												<i class="flaticon-left-arrow-1" aria-hidden="true"></i>
											</a>
										</li>
										<li v-for="link in pagination.links">
											<template v-if="Number(link.label) && pagination.current_page - link.label < 3 && pagination.current_page - link.label > -3">
												<a @click.prevent="getProducts(link.label)" :class="link.active ? 'active' : ''" href="javascript:void(0);">{{ link.label }}</a>
											</template>
										</li>
										<li v-if="pagination.current_page !== pagination.last_page">
											<a @click.prevent="getProducts(pagination.current_page + 1)" href="javascript:void(0);">
												<i class="flaticon-next-1" aria-hidden="true"></i>
											</a>
										</li>
										<li>
											<a @click.prevent="getProducts(pagination.last_page)" href="javascript:void(0);">Last</a>
										</li>
									</ul>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</main>
	</div>
</template>

<script>
export default {
	name: 'Index',
	mounted() {
		$(document).trigger('changed');
		this.getProducts();
		this.getFilterList();
	},
	data() {
		return {
			products: [],
			popupProduct: null,
			filterList: [],
			categories: [],
			colors: [],
			tags: [],
			prices: [],
			order: 'title|asc',
			pagination: [],
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
		getProducts(page = 1) {
			const data = {
				'categories': this.categories,
				'colors': this.colors,
				'tags': this.tags,
				'prices': this.prices,
				'order': this.order,
				'page': page,
			};

			this.axios.post('http://ecommerce_shop.local/api/products', data)
				.then(res => {
					this.products = res.data.data;
					this.pagination = res.data.meta;
					//console.log(res);
				})
				.finally(v => {
					$(document).trigger('init');
				});
		},
		getProduct(id) {
			this.axios.get(`http://ecommerce_shop.local/api/products/${id}`)
				.then(res => {
					this.popupProduct = res.data.data;
					//console.log(res);
				})
				.finally(v => {
					$(document).trigger('init');
				});
		},
		getFilterList() {
			this.axios.get(`http://ecommerce_shop.local/api/products/filters`)
				.then(res => {
					this.filterList = res.data;
					//console.log(res);
				});
		},
		addColor(id) {
			if (!this.colors.includes(id)) {
				this.colors.push(id);
			}
			else {
				this.colors = this.colors.filter(elem => {
					return elem !== id
				});
			}
		},
		addTag(id) {
			if (!this.tags.includes(id)) {
				this.tags.push(id);
			}
			else {
				this.tags = this.tags.filter(elem => {
					return elem !== id
				});
			}
		},
		addOrder(event) {
			this.order = event.target.value;
			this.filterProducts();
		},
		filterClear() {
			this.categories = [];
			this.colors = [];
			this.tags = [];
			this.prices = [];
			$('#price_min').val('1');
			$('#price_max').val('999');
			this.filterProducts();
		},
		filterProducts() {
			this.prices[0] = $('#price_min').val();
			this.prices[1] = $('#price_max').val();
			this.getProducts();
		},
		addToCart(product, isSingle) {
			let cart = localStorage.getItem('cart');
			let qty = isSingle ? 1 : $('#qtyValue').val();
			$('#qtyValue').val(1);

			let newProduct = [
				{
					id: product.id,
					image_url: product.images[0].file_path,
					title: product.title,
					price: product.price,
					qty: qty
				}
			];

			if (!cart) {
				localStorage.setItem('cart', JSON.stringify(newProduct));
			}
			else {
				cart = JSON.parse(cart);

				cart.forEach(productInCart => {
					if (productInCart.id === product.id) {
						productInCart.qty = Number(productInCart.qty) + Number(qty);
						newProduct = null;
					}
				})

				Array.prototype.push.apply(cart, newProduct);
				localStorage.setItem('cart', JSON.stringify(cart));
			}
		}
	}
}
</script>
