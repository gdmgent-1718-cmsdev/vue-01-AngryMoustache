<template>
    <div class="hello">
        <p>API Get</p>
        <button v-on:click="getcall('http://cmsdev.localhost/node/1?_format=hal_json')">GET</button>
        <br>
        <br>
        <br>
        <p>API Post</p>
        <input type="text" name="title" v-model="title">
        <button v-on:click="postcall('http://cmsdev.localhost/node/1?_format=hal_json')">POST</button>
    </div>
</template>

<script>

	export default {
	    name: 'App',
	    data () {
	        return {
	            title: ''
	        }
	    },
	    methods: {
	    	getcall: function (api) {
	    		Vue.axios.get(api).then((response) => {
	  				console.log(response.data)
				});
	    	},
	    	postcall: function (api) {
	    		var that = this;
	    		Vue.axios.post(api ,{
			   		method: 'post',
			   		headers: {
			   			'Accept': 'application/hal+json',
			   			'Content-Type': 'application/hal+json',
			   			'X-CSRF-Token': 'wXwMwlyuTd_MjKhgtTH2JvdChUm6h1C4iYZ8uCiNidM'
			   		},
	    			auth: {
	    				username: 'cmsdev-user',
	    				password: 'cmsdev-pass'
	    			},
	    			body: {

						  "_links": {
						    "type": {
						      "href": "http://cmsdev.localhost/rest/type/node/article"
						    }
						  },
						  "title": {
						    "value": that.title
						  },
						  "type": {
						    "target_id": "article"
						  }
	    			}
			  	}).then(function(response){
			    	console.log('Authenticated');
			  	});
	    	}
	    }
	}

</script>
