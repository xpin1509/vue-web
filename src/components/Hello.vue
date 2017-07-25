<template>
	<div class="hello">
		<div class="areaBar">
			<select name="" class="province_now input-brd" @change="provinceChange">
				<option>省/市</option>
				<option v-for="item in province_now" :value="item.code">{{item.name}}</option>
			</select>
			<select name="" class="city_now input-brd" v-on:change="cityChange">
				<option>市/区</option>
				<option v-for="item in city_now" :value="item.code">{{item.name}}</option>
			</select>
			<select name="" class="county_now input-brd">
				<option>县/市</option>
				<option v-for="item in county_now"></option>
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
				county_now: [],
				data: {},
				provinceId:0,
				cityId:0
			}
		},
		mounted: function() {
			this.$nextTick(function() {
				this.showArea();
			});
		},
		methods: {
			selectVal: function(ele) {
				this.selected = ele.target.value;
				console.log(ele)
			},
			showArea: function() {
				this.province_now = [];
				this.$http.get('static/mockup/adc-tree.json').then(function(res) {
					this.data = res.data;
					for(var key in this.data) {
						this.province_now.push(this.data[key]);
					}
				})
			},
			provinceChange: function(e) {
				this.city_now = [];
				var code = e.target.value;
				var citys = this.data[code].children;
				for(var key in citys) {
					this.city_now.push(citys[key]);
				}
			},
			cityChange: function(e) {
				this.county_now = [];
				var code = e.target.value;
				if(this.data[code].children){
					var citys = this.data[code].children;
					for(var key in citys) {
						this.county_now.push(citys[key]);
					}
				}
				
			}

			/*getCookie: function(c_name) {
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
			}*/
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