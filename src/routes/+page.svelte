<script lang="ts">
	import starIcon from '$lib/images/icon-star.svg';
	import thankYouIllustration from '$lib/images/illustration-thank-you.svg';

	let savedRating: string;
	let succesState: boolean = false;

	function onRatingClick(event: any) {
		const clickedRating = event.currentTarget;
		const ratingValue = clickedRating.textContent;

		savedRating = ratingValue;
	}

	function succesStateResponse() {
		succesState = true;

		setTimeout(() => {
			window.location.reload();
		}, 3000);
	}
</script>

{#if succesState && savedRating}
	<div class="thank-you-box text-c">
		<img src={thankYouIllustration} alt="" />
		<p class="selected-rating">You selected {savedRating} out of 5</p>
		<div class="desc">
			<h2>Thank you!</h2>
			<p>
				We appreciate you taking the time to give a rating. If you ever need more support, don't
				hesitate to get in touch!
			</p>
		</div>
	</div>
{:else}
	<div class="rating-box">
		<form>
			<div class="img-container">
				<img src={starIcon} alt="star icon" />
			</div>
			<div class="desc">
				<h1>How did we do?</h1>
				<p>
					Please let us know how we did with your support request. All feedback is appreciated to
					help us improve our offering!
				</p>
			</div>
			<div class="buttons">
				{#each { length: 5 } as _, i}
					<button id={`rating${i + 1}`} on:click={onRatingClick} type="button">{i + 1}</button>
				{/each}
			</div>
			<button class="btn" type="submit" on:click={succesStateResponse}>Submit</button>
		</form>
	</div>
{/if}

<style lang="scss">
	@import '../sass/abstracts/variables';

	.rating-box {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);

		color: $Medium;
		background: $Box;

		max-width: 430px;
		padding: 35px;
		border-radius: 30px;

		.desc {
			margin: 30px 0;

			h1 {
				color: $White;
				font-weight: 400;
			}

			p {
				line-height: 25px;
				margin-top: 10px;
			}
		}
	}

	.btn {
		width: 100%;

		cursor: pointer;

		padding: 15px 0;
		border: none;
		border-radius: 30px;

		text-transform: uppercase;

		color: $White;
		background: $Orange;
		font-size: 16px;

		letter-spacing: 3px;

		&:hover {
			color: $Orange;
			background: $White;
		}
	}

	.buttons {
		display: flex;
		justify-content: space-around;

		margin-bottom: 30px;

		button {
			cursor: pointer;
			background: $Dark;
			color: $Medium;

			font-size: 16px;
			font-weight: 700;

			width: 50px;
			height: 50px;

			border: none;
			border-radius: 50%;

			@media screen and (max-width: 995px) {
				margin: 0 8px;
				width: 45px;
				height: 45px;
			}

			&:hover {
				background: $Medium;
				color: $White;
			}

			&:focus {
				background: $Orange;
				color: $White;
			}
		}
	}

	.img-container {
		position: relative;

		width: 45px;
		height: 45px;
		border-radius: 50%;
		background: $Dark;

		img {
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
		}
	}

	.thank-you-box {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);

		background: $Box;
		color: $Medium;

		max-width: 410px;
		padding: 35px;
		border-radius: 30px;

		@media screen and (max-width: 995px) {
			min-width: 410px;
		}

		h2 {
			color: $White;
		}

		.selected-rating {
			display: inline-block;

			color: $LightOrange;
			background: $Dark;

			padding: 5px 15px;
			border-radius: 30px;
			margin-top: 20px;
		}

		p {
			line-height: 25px;
			margin-top: 10px;
		}

		.desc {
			margin-top: 30px;
		}
	}
</style>
