<template>
	<div class="hello">
		<div class="areaBar">
			<select name="" class="province_now input-brd">
				<option value="" v-for="item in province_now">{{item}}</option>
			</select>
			<select name="" class="city_now input-brd">
				<option value="" v-for="item in city_now">{{item}}</option>
			</select>
			<select name="" class="county_now input-brd">
				<option value="" v-for="item in county_now">{{item}}</option>
			</select>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'hello',
		data() {
			return {
				province_now: [],
				city_now: [],
				county_now: []
			}
		},
		mounted: function() {
			//this.checkCookie()
			this.$nextTick(function() {
				this.showArea();
			});
		},
		methods: {
			showArea: function() {
				this.$http.get('static/mockup/adc-tree.json').then(function(res) {
					console.log(res.data)
				})
			},
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
	
	.areaBar {
		line-height: 30px;
		text-align: center;
	}
	
	.input-brd {
		display: inline-block;
		width: 150px;
		height: 30px;
		margin: 10px 10px;
		border-radius: 5px;
	}
</style>