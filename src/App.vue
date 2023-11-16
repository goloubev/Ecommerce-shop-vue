<template>
	<div>
		<header class="header-style-3">
			<!-- Start Desktop Menu -->
			<div class="menubox">
				<div class="container-fluid">
					<div class="d-lg-block d-none">
						<div class="row g-0 position-relative">
							<div class="col-lg-3 d-flex align-items-center justify-content-center border-rit">
								<div class="logo">
									<a href="index.html">
										<img src="/src/assets/images/logo/logo.png" alt="">
									</a>
								</div>
							</div>
							<div class="col-lg-9 g-0 p-0">
								<div class="row g-0 holder">
									<div class="col-12">
										<div class="some-info">
											<div class="right d-flex align-items-center">
												<a href="login.html"> Sign In / Register </a>
											</div>
										</div>
									</div>
								</div>
								<div class="border-one"></div>
								<div class="row g-0 holder">
									<div class="col-12">
										<div class="mega-menu-default mega-menu d-lg-block d-none">
											<div class="d-flex align-items-center justify-content-between">
												<nav>
													<ul class="page-dropdown-menu d-flex align-items-center justify-content-center">
														<li class="dropdown-list"><router-link to="/"><span>Home</span></router-link></li>
														<li class="dropdown-list"><router-link to="/products"><span>Products</span></router-link></li>
													</ul>
												</nav>

												<div class="right d-flex align-items-center justify-content-end">
													<ul class="main-menu__widge-box d-flex align-items-center">
														<li class="d-lg-block d-none"><a href="my-account.html"><i
															class="flaticon-user"></i> </a></li>
														<li class="d-lg-block d-none"><a href="wishlist.html" class="number"><i class="flaticon-heart"></i> <span
															class="count">(2)</span> </a> </li>
														<li class="cartm"> <a href="#0" class="number cart-icon"> <i
															class="flaticon-shopping-cart"></i><span
															class="count">(5)</span> </a> </li>
													</ul>
												</div>
											</div>
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</header>

		<router-view></router-view>

		<footer class="footer-default footer-3">
			<div class="footer-default__shap_1 position-absolute">
				<img src="/src/assets/images/shape/footer-shape-1.png" alt="">
			</div>

			<!--Start Footer-->
			<div class="footer-default__main-footer position-relative">
				<div class="container">
					<div class="row">
						<div class="col-xl-3 col-lg-6 col-md-6 col-sm-12 mt-30 wow fadeInUp animated">
							<div class="footer-default__single-box">
								<div class="company-info">
									<div class="footer-title">
										<h4> Office</h4>
									</div>
									<div class="text1">
										<p>29 Holles Place, Dublin 2 D02 YY46</p>
									</div>
									<div class="text2">
										<p>68 Jay Street, Suite 902 New Side <br> Brooklyn, NY 11201</p>
									</div>
									<div class="text3">
										<p>New York, United States</p>
									</div>
								</div>
							</div>
						</div>
						<div class="col-xl-2 col-lg-6 col-md-6 col-sm-12 mt-30 wow fadeInUp animated">
							<div class="footer-default__single-box">
								<div class="footer-title">
									<h4> Useful Links </h4>
								</div>
								<ul class="footer-links">
									<li><a href="my-account.html">Account</a></li>
									<li><a href="login.html">Sign In</a></li>
									<li><a href="cart.html">View Cart</a></li>
									<li><a href="wishlist.html">My WishList</a></li>
									<li><a href="compare.html">Compare Products</a></li>
								</ul>
							</div>
						</div>
						<div class="col-xl-3 col-lg-6 col-md-6 col-sm-12 mt-30 wow fadeInUp animated">
							<div class="footer-default__single-box">
								<div class="footer-title">
									<h4> Information </h4>
								</div>
								<ul class="footer-links">
									<li><a href="about-us.html">About us</a></li>
									<li><a href="contact.html">Contact Us </a></li>
									<li><a href="faq.html">Faq</a></li>
									<li><a href="blog.html">Latest Posts</a></li>
									<li><a href="order-track.html">Order Track</a></li>
								</ul>
							</div>
						</div>
						<div class="col-xl-4 col-lg-6 col-md-6 col-sm-12 mt-30 wow fadeInUp animated">
							<div class="footer-default__single-box">
								<div class="footer-title">
									<h4> Newsletter </h4>
								</div>
								<div class="footer-newsletter">
									<p class="text">Enter your email to receive our latest updates about our products & promotions. </p>
									<form action="#0" class="footer-default__subscrib-form">
										<div class="footer-input-box">
											<input type="email" placeholder="Email address" name="email">
											<button type="submit" class="subscribe_btn"> Subscribe</button>
										</div>
									</form>
									<div class="newsletter-bottom d-flex align-items-center">
										<div class="footer-title-box">
											<p>Follow Us:</p>
										</div>
										<div class="footer__medio-boxx  medio-boxx  d-flex align-items-center">
											<ul>
												<li><a href="https://www.facebook.com/" target="_blank" class="active"><i class="flaticon-facebook-app-symbol"></i></a></li>
												<li><a href="https://www.youtube.com/" target="_blank"><i class="flaticon-youtube"></i></a></li>
												<li><a href="https://twitter.com/"><i class="flaticon-twitter" target="_blank"></i></a></li>
												<li><a href="https://www.instagram.com/"><i class="flaticon-instagram" target="_blank"></i></a></li>
											</ul>
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div> <!-- footer-bottom Footer-->
			<div class="footer_bottom position-relative">
				<div class="container">
					<div class="footer_bottom_content">
						<div class="copyright wow fadeInUp animated">
							<p>© 2022 <a href="index.html">Karte.</a> All Rights Reserved.</p>
						</div>
						<div class="footer-payment wow fadeInUp animated">
							<a href="#0"> <img src="/src/assets/images/home-four/method-1.jpg" alt="payment"> </a>
							<a href="#0"> <img src="/src/assets/images/home-four/method-2.jpg" alt="payment"> </a>
							<a href="#0"> <img src="/src/assets/images/home-four/method-3.jpg" alt="payment"> </a>
							<a href="#0"> <img src="/src/assets/images/home-four/method-4.jpg" alt="payment"> </a>
						</div>
					</div>
				</div>
			</div>
		</footer>
	</div>
</template>

<script>
export default {
	name: 'App',
	mounted() {
		$(document).trigger('init')
	}
}
</script>
