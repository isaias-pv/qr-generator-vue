<template>
    <div class="container border pt-2">
        <div class="row">
            <div class="col-lg-12">
                <img :src="img" class="img-thumbnail" alt="">
            </div>
        </div>
        <div class="row">
            <div class="col-lg-6">siaias</div>
            <div class="col-lg-6">sadns</div>
        </div>
    </div>
</template>


<script>
import QRCode from 'qrcode';

export default {
    props: ['param'],
    data() {
        return{ 
            img: ""
        }
    },
    methods: {
        loadQr(){
            QRCode.toDataURL(this.param, {
				width: 800,
				margin: 2,
				color: {
					dark: '#335383FF',
					light: '#EEEEEEFF'
				}
			}, (err, url) => {
				if (err) return console.error(err)
				console.log(url)
				this.img = url
			})
        }
    },
    mounted(){
        this.loadQr();
    }
}
</script>

<style scoped>
    .border{
        border-radius: 15px;
    }
</style>