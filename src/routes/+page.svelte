<script>
	const API_BASE = "https://nackademin-item-tracker.herokuapp.com/";
	let testObject = {
		listname: "Henrik's test list 3",
		itemList: [
			{
				listName: "my user's list",
				shoppingItems: [
					{ name: "banana", amount: 5, done: true },
					{ name: "cow", amount: 3, done: false },
				],
			},
			{
				listName: "my user's second list",
				shoppingItems: [
					{ name: "cucumbers", amount: 2, done: true },
					{ name: "ducks", amount: 10, done: false },
				],
			},
		],
	};
	async function searchList(inputlist) {
		const query = inputlist;
		const res = await fetch(`${API_BASE}listsearch?listname=${query}`);
		const data = await res.json();
		console.log(data);
		return data;
	}

	async function createList(inputlist) {
		const res = await fetch(`${API_BASE}lists`, {
			method: "POST",
			headers: {
				"Content-Type": "application/json",
			},
			body: JSON.stringify(testObject),
		});

		const { list } = await res.json();
		currentList = list._id;
	}
	async function addItem(inputlist) {
		currentList = "63e51467725e914d6005b761";
		if (!currentList) {
			return alert("Choose a list");
		}

		if (!itemTitleField || !itemDescField) {
			return alert("Fill text boxes");
		}

		const res = await fetch(`${API_BASE}lists/${currentList}/items`, {
			method: "POST",
			headers: {
				"Content-Type": "application/json",
			},
			body: JSON.stringify({
				title: itemTitleField,
				description: itemDescField,
			}),
		});
		// const { list } = await res.json();
	}

	$: lists = "";
	let items;
	let searchListValue;
	let createListValue;
	let itemTitleField;
	let itemDescField;
	let currentList;
</script>

<div class="flex w-64 flex-col">
	<form on:submit={async () => (lists = await createList())} class="m-4 [&>*]:m-1" id="create-list">
		<label for="create-list-name">Create listname</label>
		<input
			bind:value={createListValue}
			class="rounded-md rounded-md border p-1 p-1"
			id="create-list-name"
			type="text" />
		<button class="rounded-lg bg-blue-500 p-1 text-white hover:bg-blue-400">Create</button>
	</form>
	<hr />
	<form
		on:submit={async () => (lists = await searchList(searchListValue))}
		class="m-4 [&>*]:m-1"
		id="list-search">
		<label for="list-name">Listname</label>
		<input bind:value={searchListValue} class="rounded-md border p-1" id="list-name" type="text" />
		<button class="rounded-lg bg-blue-500 p-1 text-white hover:bg-blue-400">Search</button>
	</form>
	<ul id="lists" />
	<hr />
	<form class="m-4 [&>*]:m-1" id="update-list">
		<input class="rounded-md border p-1" id="listname" type="text" />
		<button class="rounded-lg bg-blue-500 p-1 text-white hover:bg-blue-400">Update Name</button>
	</form>
	<ul id="item-list" />
	<hr />
	<form on:submit={() => addItem()} class="m-4 [&>*]:m-1" id="add-item">
		<label for="item-title">Title:</label>
		<input bind:value={itemTitleField} class="rounded-md border p-1" id="item-title" type="text" />
		<br />
		<label for="item-desc">Description:</label>
		<textarea bind:value={itemDescField} class="rounded-md border p-1" id="item-desc" />
		<br />
		<button class="rounded-lg bg-blue-500 p-1 text-white hover:bg-blue-400">Save</button>
	</form>
</div>

<div>
	{#each Object.entries(lists) || [] as [keys, list]}
		<div class="m-4  rounded-xl bg-slate-300 p-2">
			<p>_id: {list._id}</p>
			<p>List name: {list.listname}</p>
			<ul class="m-8">
				{#each list.itemList || [] as item}
					<li class="m-2 rounded-xl bg-slate-200 p-2">
						<h4>Title: {item.title}</h4>
						<p>Desc: {item.description}{item.checked ? "✅" : ""}</p>
					</li>
				{/each}
			</ul>
		</div>
	{/each}
</div>

<style>
</style>
