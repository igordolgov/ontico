<template>
	<footer class="footer">
		<div class="container">
			<div class="footer__information">
				<div class="footer__contacts">
					<div class="footer__title">По любым вопросам обращайтесь:</div>

					<div class="footer__elem">
						<span class="footer__title">Бухгалтерия и вопросы оплаты :</span>
						<a href="mailto:support@ontico.ru">support@ontico.ru</a> +7(495)646-07-68,
						<a href="https://t.me/ontico_support">@ontico_support</a>
					</div>

					<div class="footer__elem">
						<span class="footer__title">Программный комитет :</span>
						<a href="mailto:speakers@ontico.ru">speakers@ontico.ru</a>
					</div>

					<div class="footer__elem">
						<span class="footer__title">Организационный комитет :</span>
						<a href="mailto:organization@ontico.ru">organization@ontico.ru</a>
					</div>

					<div class="footer__elem">
						125040, г.Москва, ул.Нижняя, д.14, стр.7, под.1, эт.2, офис 08, ООО
						«Конференции Олега Бунина»
					</div>
				</div>
				<img class="footer__year-img" src="images/year.svg" alt="year-logo" />
			</div>
		</div>

		<div class="footer__calendar">

		<div class="footer__calendar-year">2022 год:</div>
			<ul
				v-for="(month,index) in footerMonths" :key="index"
				class="footer__months">
				<li class="footer__month">{{ month }}</li>
			</ul>
		</div>
	</footer>
</template>

<script>
export default {
	name: "AppFooter",

	data() {
		return {
			footerMonths: [
				"январь", "февраль", "март", "апрель", "май", "июнь", "июль", "август", "сентябрь", "октябрь", "ноябрь", "декабрь"
			]
		}
	},
};
</script>

<style scoped>
	.footer {
		font-size: 18px;
		background-color: #262529;
		color: #fff;
		font-family: TTTravels, Arial, Helvetica, sans-serif;
	}

	.footer__title {
		font-weight: bold;
		margin: 10px 0 5px;
	}

	.footer__elem:not(:last-child) {
		margin-bottom: 20px;
	}

	.footer__elem a {
		font-weight: normal;
		color: #fff;
	}

	.footer__information {
		flex-wrap: wrap;
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 10px;
	}

	.footer__contacts {
		max-width: 590px;
	}

	.footer__year-img {
		margin-bottom: 24px;
		max-width: 100%;
	}

	.footer__calendar {
		background-color: #414141;
		opacity: .85;
		border-top: 1px solid #fff;
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		width: 100%;
		padding: 0 24px 24px;
	}

	.footer__calendar-year {
		font-weight: bolder;
		font-size: 36px;
		line-height: 43px;
	}

	.footer__months {
		display: flex;
		flex-direction: row;
		list-style: none;
		font-weight: bold;
		font-family: TTTravels, Arial, Helvetica, sans-serif;
	}

	.footer__month {
		padding-top: 15px;
		margin-left: 12px;
		position: relative;
	}

	.footer__month:nth-child(5)::before {
		content: "";
		background-image: url('/assets/Rectangle.svg');
		background-color: #000;
		height: 10px;
		left: 53px;
		position: absolute;
		top: -5px;
		width: 35px;
	}

	.footer__month+.footer__month {
		padding-left: 50px;
	}

	@media (max-width: 1570px) {
		.footer__information {
			flex-direction: column;
			justify-content: center;
		}

		.footer__contacts {
			margin-bottom: 30px;
		}

		.footer__year-img {
			max-width: 70%;
		}
	}
</style>