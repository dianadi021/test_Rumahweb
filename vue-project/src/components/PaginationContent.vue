<script>
async function submitForm() {
  $("#loadingAjax").show();
	toastr.warning("Sedang mengirim data", "Perhatian!!");
	await axios
		.post("https://jsonplaceholder.typicode.com/posts")
		.then(function (callback) {
			console.log(callback);
			const { data } = callback;
			datas.value = data;

			$("#loadingAjax").hide();
			toastr.success("Data berhasil terkirim", "Sukses!!");
		})
		.catch(function ($error) {
			console.log("Error: ", $error);
			$("#loadingAjax").hide();
			toastr.error("Kesalahan mengirim data", "Kesalahan!!");
		});
}
</script>

<template>
  <div>
    <form id="inputUser" @submit.prevent="submitForm">
      <label for="username">Userusername:</label>
      <input type="text" id="username" username="username" v-model="username" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
      <label for="password">Password:</label>
      <textarea id="password" namae="password" v-model="password" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm" style="resize: none;"></textarea>
      <button type="submit" class="w-full bg-blue-500 text-white font-medium py-2 px-4 rounded-lg shadow-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">Submit</button>
    </form>
  </div>
</template>