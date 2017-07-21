<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<h2>Essential Links</h2>
	</div>
</template>

<script>
	export default {
		name: 'hello',
		data() {
			return {
				msg: 'Welcome to Your Vue.js App'
			}
		},
		mounted: function() {
			//this.checkCookie()
		},
		methods: {
			getCookie: function(c_name) {
				if(document.cookie.length > 0) {
					c_start = document.cookie.indexOf(c_name + "=")
					if(c_start != -1) {
						c_start = c_start + c_name.length + 1
						c_end = document.cookie.indexOf(";", c_start)
						if(c_end == -1) c_end = document.cookie.length
						return unescape(document.cookie.substring(c_start, c_end))
					}
				}
				return ""
			},

			setCookie: function(c_name, value, expiredays) {
				var exdate = new Date();
				exdate.setDate(exdate.getDate() + expiredays);
				document.cookie = c_name + "=" + escape(value) +
					((expiredays == null) ? "" : ";expires=" + exdate.toGMTString())
			},

			checkCookie: function() {
				username = getCookie('username')
				if(username != "") {
					alert('Welcome again ' + username + '!')
				} else {
					username = prompt('Please enter your name:', "")
					if(username != "") {
						setCookie('username', username, 365)
					}
				}
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	h1,
	h2 {
		font-weight: normal;
	}
	
	ul {
		list-style-type: none;
		padding: 0;
	}
	
	li {
		display: inline-block;
		padding: 0 10px;
	}
	
	a {
		color: #42b983;
	}
</style>