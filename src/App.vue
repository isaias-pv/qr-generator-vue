<script>
import { RouterLink, RouterView } from 'vue-router'
import HomeViewVue from './views/HomeView.vue'
import NavbarComponent from './components/NavbarComponent.vue'

export default {
  	components: {
		HomeViewVue,
	    NavbarComponent
	}
}

</script>

<template>
    <NavbarComponent/>
    	
      		<HomeView />
    	
  	<RouterView />
</template>