<script>
	import Split from "../components/split_table.svelte";

	let average;
</script>

<main>
	<div class="hero is-fullheight-with-navbar header-image">
		<div class="hero-body">
			<div class="container">
				<div class="columns has-text-centered">
					<div class="column">
						<Split />
					</div>
				</div>
			</div>
		</div>
	</div>
</main>

<style>
	.header-image {
		position: relative;
		background-image: url("../background.jpg");
		background-position: center center;
		background-repeat: no-repeat;
		background-attachment: fixed;
		background-size: cover;
		background-color: #999;
	}
	.header-image::before {
		content: "";
		position: absolute;
		top: 0px;
		right: 0px;
		bottom: 0px;
		left: 0px;
		background-color: rgba(0, 0, 0, 0.3);
	}
</style>
