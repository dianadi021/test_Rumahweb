<script setup>
import FormInput from "../components/FormInput.vue";
import FormLogin from "../components/FormLogin.vue";

import { ref } from "vue";
import axios from "axios";

let datas = ref([]);
async function ContentLoader() {
	$("#loadingContetLoader").show();
	toastr.warning("Sedang mengambil data", "Perhatian!!");
	await axios
		.get("https://jsonplaceholder.typicode.com/users")
		.then(function (callback) {
			console.log(callback);
			const { data } = callback;
			datas.value = data;

			$("#loadingContetLoader").hide();
			toastr.success("Data berhasil diambil", "Sukses!!");
		})
		.catch(function ($error) {
			console.log("Error: ", $error);
			$("#loadingContetLoader").hide();
			toastr.error("Kesalahan mengambil data", "Kesalahan!!");
		});
}

(async function () {
	await ContentLoader();
})();
</script>

<template>
	<div class="w-full">
		<div id="container-content" class="w-full">
			<ul v-for="list in datas" :key="list.id">
				<li>{{ list.name }}</li>
			</ul>
		</div>
		<div class="form-container w-full">
			<FormInput />
			<FormLogin />
		</div>
	</div>
</template>
