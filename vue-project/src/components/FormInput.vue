<script setup>
import { ref } from "vue";
import axios from "axios";

let datas = ref([]);
async function submitForm() {
	if (!$("#name").val()) {
		toastr.warning("Nama harus di isi", "Perhatian!!");
		$("#name").focus();
		return false;
	}

	if (!$("#email").val()) {
		toastr.warning("Email harus di isi", "Perhatian!!");
		$("#email").focus();
		return false;
	}

	if (!$("#message").val()) {
		toastr.warning("Message harus di isi", "Perhatian!!");
		$("#message").focus();
		return false;
	}

  const formDatas = {
    name: $("#name").val(),
		email: $("#email").val(),
		message: $("#message").val(),
  }

	$("#loadingAjax").show();
	toastr.warning("Sedang mengirim data", "Perhatian!!");
	await axios
		.post("https://jsonplaceholder.typicode.com/posts", formDatas)
		.then(function (callback) {
			console.log(callback);

			datas.value.push(formDatas)
			console.log(datas.value);
			

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
	<div class="w-full">
		<form id="inputUser">
			<label for="name">Nama:</label>
			<input type="text" id="name" name="name" v-model="name" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
			<label for="email">Email:</label>
			<input type="email" id="email" name="email" v-model="email" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
			<label for="message">Pesan:</label>
			<textarea id="message" namae="message" v-model="message" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm" style="resize: none"></textarea>
		</form>
		<button @click="submitForm" class="w-full bg-blue-500 text-white font-medium py-2 px-4 rounded-lg shadow-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">Submit</button>

		<div class="w-full">
			<ul v-if="datas.value" v-for="list in datas.value" :key="list.id">
				<li>{{ list.email }}</li>
			</ul>
		</div>
	</div>
</template>
