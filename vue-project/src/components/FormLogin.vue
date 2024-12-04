<script setup>
import axios from "axios";

async function submitForm() {
	if (!$("#username").val()) {
		toastr.warning("Username harus di isi", "Perhatian!!");
		$("#username").focus();
		return false;
	}

	if (!$("#password").val()) {
		toastr.warning("Password harus di isi", "Perhatian!!");
		$("#password").focus();
		return false;
	}

  const formDatas = {
    username: $("#username").val(),
		password: $("#password").val()
  }

	$("#loadingAjax").show();
	toastr.warning("Sedang mencoba login", "Perhatian!!");
	await axios
		.post("https://jsonplaceholder.typicode.com/login")
		.then(function (callback) {
			console.log(callback);

			$("#loadingAjax").hide();
			toastr.success("Berhasil login", "Sukses!!");
		})
		.catch(function ($error) {
			console.log("Error: ", $error);
			$("#loadingAjax").hide();
			toastr.error("Gagal login", "Kesalahan!!");
		});
}
</script>

<template>
  <div class="w-full">
    <form id="inputUser" @submit.prevent="submitForm">
      <label for="username">Username:</label>
      <input type="text" id="username" username="username" v-model="username" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
      <label for="password">Password:</label>
      <input type="password" id="password" namae="password" v-model="password" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm" />
    </form>
    <button @click="submitForm" class="w-full bg-blue-500 text-white font-medium py-2 px-4 rounded-lg shadow-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">Login</button>
  </div>
</template>