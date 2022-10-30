<script>
	const formatter = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',

  // These options are needed to round to whole numbers if that's what you want.
  //minimumFractionDigits: 0, // (this suffices for whole numbers, but will print 2500.10 as $2,500.1)
  //maximumFractionDigits: 0, // (causes 2500.99 to be printed as $2,501)
	});
	let loan = 200_000
	let years = 15
	let interestRateInput = 2000
	$: interestRate = interestRateInput / 100 
	$: intereerer = interestRate / 100 + 1
	$: totalPayments = years * 12;
	$: monthlyInterestRate = interestRate / 100 / 12
	$: monthlyPayment = (loan * Math.pow(intereerer, years) / totalPayments).toFixed(2)

</script>

<main class="container">
	<div class="row"><h1>Morgage Calc</h1></div>
	<div class="row">
		<label for="loanInput">Loan amount:</label>
		<input name="loanInput" bind:value={loan} type="number" class="u-full-width" min="1" placeholder="Enter loan Amount">
	</div>
	<div class="row">
		<div class="columns six">
			<label for="year">Years:</label>
			<input type="range" bind:value={years} min="1" name="year" max="50" class="u-full-width">
		</div>
		<div class="columns six outputs">
			{years} Years
		</div>
	</div>
	<div class="row">
		<div class="columns six">
			<label for="year">Interest Rate:</label>
			<input type="range" bind:value={interestRateInput} min="1" name="year" max="2000" class="u-full-width">
		</div>
		<div class="columns six outputs">
			{interestRate.toFixed(2)} %
		</div>
	</div>
	<div class="row outputs">Monthly Payments: {formatter.format(monthlyPayment)}</div>
	<div class="row outputs">Total Payments: {totalPayments}</div>
	<div class="row outputs">Total Paid: {formatter.format(monthlyPayment * years * 12)}</div>
</main>

<style>
	.outputs {
		font-size: 20px;
		border: solid black 2px;
		margin-top: 15px;
		text-align: center;
	}
</style>