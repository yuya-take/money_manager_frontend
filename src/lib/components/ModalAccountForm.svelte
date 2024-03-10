<script lang="ts">
	// Stores
	import { getModalStore } from '@skeletonlabs/skeleton';

	import { DateInput } from 'date-picker-svelte'

	// Props

	const modalStore = getModalStore();

	const formData = {
		date: new Date(),
		category: '',
		amount: '',
		description: '',
		paymentMethod: '',
		recurring: 'none'
	};

	// Functions
	function onFormSubmit(): void {
		if ($modalStore[0].response) $modalStore[0].response(formData);
		modalStore.close();
	}

	const cBase = 'card p-4 w-modal shadow-xl space-y-4';
	const cHeader = 'text-2xl font-bold';
	const cForm = 'border border-surface-500 p-4 space-y-4 rounded-container-token';
</script>

{#if $modalStore[0]}
	<div class="{cBase}">
		<header class={cHeader}>{$modalStore[0].title ?? 'Add Expense/Income Record'}</header>
		<article>{$modalStore[0].body ?? 'Please fill in the details below to add a new record.'}</article>
		<form class="{cForm}">
			<label class="label" for="date">
				<span>Date</span>
				<DateInput id="date" bind:value={formData.date} format="yyyy-MM-dd" closeOnSelection={true} />
			</label>
			<label class="label">
				<span>Category</span>
				<input class="input" type="text" bind:value={formData.category} placeholder="Category..." />
			</label>
			<label class="label">
				<span>Amount</span>
				<input class="input" type="number" bind:value={formData.amount} placeholder="Amount..." />
			</label>
			<label class="label">
				<span>Description</span>
				<textarea class="textarea" bind:value={formData.description} placeholder="Description (Optional)..."></textarea>
			</label>
			<label class="label">
				<span>Payment Method</span>
				<select class="select" bind:value={formData.paymentMethod}>
					<option value="">Select...</option>
					<option value="cash">Cash</option>
					<option value="creditCard">Credit Card</option>
					<option value="bankTransfer">Bank Transfer</option>
					<!-- 他の支払い方法を追加可能 -->
				</select>
			</label>
			<label class="label">
				<span>繰り返し</span>
				<div class="flex items-center space-x-4 mt-2">
					<label class="flex items-center space-x-2">
						<input type="radio" name="recurring" value="none" bind:group={formData.recurring} checked />
						<p>なし</p>
					</label>
					<label class="flex items-center space-x-2">
						<input type="radio" name="recurring" value="daily" bind:group={formData.recurring} />
						<p>毎日</p>
					</label>
					<label class="flex items-center space-x-2">
						<input type="radio" name="recurring" value="weekly" bind:group={formData.recurring} />
						<p>毎週</p>
					</label>
					<label class="flex items-center space-x-2">
						<input type="radio" name="recurring" value="monthly" bind:group={formData.recurring} />
						<p>毎月</p>
					</label>
				</div>
			</label>
		</form>
		<footer class="modal-footer">
			<button class="btn" on:click={modalStore.close}>Cancel</button>
			<button class="btn" on:click={onFormSubmit}>Submit</button>
		</footer>
	</div>
{/if}