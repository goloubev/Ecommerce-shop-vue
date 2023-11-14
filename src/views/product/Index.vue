<template>
	<div>
		<main class="overflow-hidden">
			<!--Start Breadcrumb Style2-->
			<div class="breadcrumb-area" style="background-image: url(/src/assets/images/inner-pages/breadcum-bg.png);">
				<div class="container">
					<div class="row">
						<div class="col-xl-12">
							<div class="breadcrumb-content pb-60 text-center">
								<h2>Shop grid</h2>
								<div class="breadcrumb-menu">
									<ul>
										<li><a href="index.html"><i class="flaticon-home pe-2"></i>Home</a></li>
										<li><i class="flaticon-next"></i></li>
										<li class="active">Shop grid</li>
									</ul>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
			<!--End Breadcrumb Style2-->
			<!--Start Product Categories One-->
			<section class="product-categories-one pb-60">
				<div class="container">
					<div class="row">
						<div class="col-xl-12">
							<div class="product-categories-one__inner">
								<ul>
									<li>
										<a href="javascript:;" class="img-box">
											<div class="inner">
												<img src="/src/assets/images/shop/product-categories-v1-img2.png" alt="" />
											</div>
										</a>
										<div class="title">
											<a href="javascript:;">
												<h6>Accessories</h6>
											</a>
										</div>
									</li>
									<li>
										<a href="javascript:;" class="img-box">
											<div class="inner">
												<img src="/src/assets/images/shop/product-categories-v1-img2.png" alt="" />
											</div>
										</a>
										<div class="title">
											<a href="javascript:;">
												<h6>Furnitures</h6>
											</a>
										</div>
									</li>
									<li>
										<a href="javascript:;" class="img-box">
											<div class="inner">
												<img src="/src/assets/images/shop/product-categories-v1-img2.png" alt="" />
											</div>
										</a>
										<div class="title">
											<a href="javascript:;">
												<h6>Jewellery</h6>
											</a>
										</div>
									</li>
								</ul>
							</div>
						</div>
					</div>
				</div>
			</section>
			<!--End Product Categories One-->
			<!--Start product-grid-->
			<div class="product-grid pt-60 pb-120">
				<div class="container">
					<div class="row gx-4">
						<div class="col-xl-3 col-lg-4">
							<div class="shop-grid-sidebar"><button class="remove-sidebar d-lg-none d-block"><i
								class="flaticon-cross"></i></button>
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
												<a href="javascript:;"
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
												<a href="javascript:;"
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
												<div v-for="product in products" class="col-xl-4 col-lg-6 col-6">
													<div class="products-three-single w-100 mt-30">
														<div class="products-three-single-img">
															<a href="javascript:;" class="d-block">
																<!-- :src !!!!! -->
																<img :src="product.images[0].file_path" alt="" />
															</a>
															<a href="javascript:;" class="addcart btn--primary style2">Add to cart</a>
															<div class="products-grid__usefull-links">
																<ul>
																	<li>
																		<a href="javascript:;"><i class="flaticon-heart"></i>
																			<span>Wishlist</span>
																		</a>
																	</li>
																	<li>
																		<a href="javascript:;">
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
																						<a @click.prevent="getProduct(groupProduct.id)" v-for="color in groupProduct.colors" :style="`background:${color.title};`" href="javascript:;" class="color-name"></a>
																					</template>
																				</div>
																			<div class="add-product">
																				<h6>Qty:</h6>
																				<div class="button-group">
																					<div class="qtySelector text-center">
	                                                                                    <span class="decreaseQty">
		                                                                                    <i class="flaticon-minus"></i>
	                                                                                    </span>
																						<input type="number" class="qtyValue" value="1" />
																						<span class="increaseQty">
																							<i class="flaticon-plus"></i>
																						</span>
																					</div>
																					<button class="btn--primary">
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
															<h5><a href="javascript:;">{{ product.title }}</a></h5>
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
							<!--<div class="row">
								<div class="col-12 d-flex justify-content-center">
									<ul class="pagination text-center">
										<li class="next"><a href="javascript:;"><i class="flaticon-left-arrows" aria-hidden="true"></i></a></li>
										<li><a href="javascript:;">1</a></li>
										<li><a href="javascript:;" class="active">2</a></li>
										<li><a href="javascript:;">3</a></li>
										<li><a href="javascript:;">...</a></li>
										<li><a href="javascript:;">10</a></li>
										<li class="next"><a href="javascript:;"><i class="flaticon-next-1" aria-hidden="true"></i></a></li>
									</ul>
								</div>
							</div>-->
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
		$(document).trigger('init'),
		this.getProducts(),
		this.getFilterList()
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
		}
	},
	methods: {
		getProducts() {
			this.axios.post('http://ecommerce_shop.local/api/products')
				.then(res => {
					this.products = res.data.data;
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
				})
				.finally(v => {
					$(document).trigger('init');
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

			this.axios.post('http://ecommerce_shop.local/api/products', {
				'categories': this.categories,
				'colors': this.colors,
				'tags': this.tags,
				'prices': this.prices,
				'order': this.order,
			})
			.then(res => {
				this.products = res.data.data;
				//console.log(res);
			})
			.finally(v => {
				$(document).trigger('init');
			});
		},
	}
}
</script>
