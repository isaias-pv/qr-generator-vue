<script setup>
import QRCode from 'qrcode';
import { onMounted } from 'vue';
import { reactive } from 'vue'

onMounted(() => {
	loadQr();
})

const state = reactive({ img: '', index: 0 })

setTimeout(() => {	
	$(document).ready(function(){
		$("#tabOptions li:eq(0) a").tab("show");
	});
}, 250);

const options = [
			{
				href: "#link",
				title: "Link",
				icon: "fa-solid fa-link"
			},
			{
				href: "#text",
				title: "Text",
				icon: "fa-solid fa-align-left"
			},
			{
				href: "#email",
				title: "Email",
				icon: "fa-solid fa-at"
			},
			{
				href: "#msg",
				title: "SMS",
				icon: "fa-solid fa-message"
			}
		]

const data = {
		url  : '',
		text : '',
		email: { to: '', sub: '', body: '' },
		msg  : { to: '', msg: '' }
	}

const structure = {
	url: "url text",
	text: "text",
	email: "MATMSG:TO:example@correo.com;SUB:hola mundo;BODY: hola mundo boy;;",
	msg: "SMSTO:129313813:sadinmasinasinsadns",
	wifi: "WIFI:T:wpa;S:Network name;P:Password;H:false;",
	tel: "tel:+573004179850",
	wha: "https://wa.me/3004179850/?text=hola mundo"
}


function loadStructure(){
	const re = [
				data.url, // URL
				data.text, // Text
				`MATMSG:TO:${data.email.to};SUB:${data.email.sub};BODY:${data.email.body};;`, // Email MATMSG:TO:example@correo.com;SUB:hola mundo;BODY: hola mundo boy;;
				`SMSTO:+${data.msg.to}:${data.msg.msg}` //SMS SMSTO:129313813:sadinmasinasinsadns
			]

			return re[Number(document.getElementsByClassName('active')[0]?.id || 0)];
}

function loadQr() {
	QRCode.toDataURL(loadStructure() || 'Not content', {
		width: 800,
		margin: 2,
		color: {
			dark: '#335383FF',
			light: '#EEEEEEFF'
		}}, (err, url) => {
			if (err) return console.error(err)
			state.img = url
	})
}

</script>

<template>
  	<div class="container mt-4 text-center">
  		<div class="row">
    		<div class="col-lg-7 col-sm-12 mr-2">
				<ul class="nav nav-pills justify-content-center" id="tabOptions">
					<li class="nav-item" v-for="option, index in options">
						<a :href="option.href" class="nav-link" data-bs-toggle="tab" :id="index">
							<i :class="option.icon"></i>
							{{option.title}}</a>
					</li>
				</ul>

				<div class="tab-content h-75 pt-4">
					
					<div class="tab-pane fade" id="link">
						<div class="form-group">
						    <input type="text" class="form-control" placeholder="Url" v-model="data.url">
  						</div>
					</div>
					
					<div class="tab-pane fade" id="text">
						<div class="form-group">
						    <input type="text" class="form-control" placeholder="Text" v-model="data.text">
  						</div>
					</div>
					
					<div class="tab-pane fade" id="email">
						<form>
  							<div class="form-group">
    							<input type="email" class="form-control" placeholder="Email" v-model="data.email.to">
  							</div>
  							<div class="form-group">
    							<input type="text" class="form-control" placeholder="Subject" v-model="data.email.sub">
							</div>
							<div class="form-group">
							    <textarea class="form-control" rows="3" placeholder="Content Email" v-model="data.email.body"></textarea>
  							</div>
						</form>
					</div>

					<div class="tab-pane fade" id="msg">
						<div class="form-group">
    						<input type="number" class="form-control" placeholder="Number" v-model="data.msg.to">
  						</div>
  						<div class="form-group">
    						<textarea class="form-control" rows="3" placeholder="Content MSG..." v-model="data.msg.msg"></textarea>
						</div>
					</div>
				</div>

				<div>
					<button class="btn btn-lg btn-primary" @click="loadQr('link')">Generar Qr</button>
				</div>
    		</div>
    		<div class="col-lg-4 col-sm-12">
				<div class="container border pt-2">
					<div class="row">
						<div class="col-lg-12">
							<img :src="state.img" class="img-thumbnail" alt="">
						</div>
					</div>
					<div class="row">
						<div class="col-lg-6">siaias</div>
						<div class="col-lg-6">sadns</div>
					</div>
				</div>
    		</div>

  		</div>
	</div>
</template>


<style>
.form-group{
	margin: 5px
}
</style>