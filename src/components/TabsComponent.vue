<template>
	<ul class="nav nav-pills justify-content-center" id="tabOptions">
		<li class="nav-item" v-for="option in options">
            <a :href="option.href" class="nav-link" data-bs-toggle="tab">
				<i :class="option.icon"></i>
				{{option.title}}</a>
        </li>
	</ul>

	<div class="tab-content h-5">
        <div class="tab-pane fade" id="link">
             <div class="form-outline mt-4">
    			<input type="email" id="form3Example3" class="form-control" :placeholder="data.link.placeholder" v-model="data.link.url"/>
    			<label class="form-label" for="form3Example3">URL</label>
  			</div>
        </div>


        <div class="tab-pane fade" id="profile">
            <h4 class="mt-2">Profile tab content</h4>
            <p>Vestibulum nec erat eu nulla rhoncus fringilla ut non neque. Vivamus nibh urna, ornare id gravida ut, mollis a magna. Aliquam porttitor condimentum nisi, eu viverra ipsum porta ut. Nam hendrerit bibendum turpis, sed molestie mi fermentum id. Aenean volutpat velit sem. Sed consequat ante in rutrum convallis. Nunc facilisis leo at faucibus adipiscing.</p>
        </div>
        <div class="tab-pane fade" id="messages">
            <h4 class="mt-2">Messages tab content</h4>
            <p>Donec vel placerat quam, ut euismod risus. Sed a mi suscipit, elementum sem a, hendrerit velit. Donec at erat magna. Sed dignissim orci nec eleifend egestas. Donec eget mi consequat massa vestibulum laoreet. Mauris et ultrices nulla, malesuada volutpat ante. Fusce ut orci lorem. Donec molestie libero in tempus imperdiet. Cum sociis natoque penatibus et magnis.</p>
        </div>
    </div>

	<div>
		<button class="btn btn-lg btn-primary" @click="sendInfo()">Generar Qr</button>
	</div>
</template>

<script>
export default{
	data: () => ({
		options: [
			{
				href: "#link",
				title: "Link",
				icon: "fa-solid fa-link"
			},
			{
				href: "#text",
				title: "Text",
				icon: "fa-solid fa-message"

			}
		],
		data: {
			link: {
				url: "",
				placeholders: "http://localhost.com/"
			}
		}
	}),
	methods: {
		sendInfo(){
			this.$emit('sendInfo', this.data.link.url);
		}
	}
}

setTimeout(() => {	
	$(document).ready(function(){
		$("#tabOptions li:eq(0) a").tab("show");
	});
}, 250);
</script>
