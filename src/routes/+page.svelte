<script>
	const API_BASE = "https://nackademin-item-tracker.herokuapp.com/";

  

</script>

<div class="flex w-64 flex-col">
	<form class="m-4 [&>*]:m-1" id="create-list">
		<label for="create-list-name">Create listname</label>
		<input class="rounded-md rounded-md border p-1 p-1" id="create-list-name" type="text" />
		<button class="rounded-lg bg-blue-500 p-1 text-white hover:bg-blue-400">Create</button>
	</form>
	<hr />
	<form class="m-4 [&>*]:m-1" id="list-search">
		<label for="list-name">Listname</label>
		<input class="rounded-md border p-1" id="list-name" type="text" />
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
	<form class="m-4 [&>*]:m-1" id="add-item">
		<label for="item-title">Title:</label>
		<input class="rounded-md border p-1" id="item-title" type="text" />
		<br />
		<label for="item-desc">Description:</label>
		<textarea class="rounded-md border p-1" id="item-desc" />
		<br />
		<button class="rounded-lg bg-blue-500 p-1 text-white hover:bg-blue-400">Save</button>
	</form>
</div>

<style>
</style>
