<template>
	<view class="index-page">
		<r-canvas ref="rCanvas"></r-canvas>
	</view>
</template>
<script>
	import rCanvas from "@/components/r-canvas/r-canvas.vue"
	export default{
		components:{
			rCanvas
		},
		data(){
			return{
				
			}
		},
		onLoad(){
			this.$nextTick(async ()=>{
				// 初始化
				await this.$refs.rCanvas.init({
					canvas_id:"rCanvas",
					// hidden:true, //是否隐藏canvas画布
					// canvas_width:300,
					canvas_height:630,
					// background_color:"red"
				})
				
				// 画背景图
				await this.$refs.rCanvas.drawImage({
					url:"/static/product_poster.png",
					x:0,
					y:0,
					w:375,
					h:630
				}).catch(err_msg=>{
					uni.showToast({
						title:err_msg,
						icon:"none"
					})
				})
				
				// 画商品图
				await this.$refs.rCanvas.drawImage({
					url:"/static/2_P_1606688103307.jpg",
					x:0,
					y:0,
					w:375,
					h:375
				}).catch(err_msg=>{
					uni.showToast({
						title:err_msg,
						icon:"none"
					})
				})
				
				// 画二维码图
				await this.$refs.rCanvas.drawImage({
					url:"/static/ercode.png",
					x:246,
					y:460,
					w:112,
					h:112
				}).catch(err_msg=>{
					uni.showToast({
						title:err_msg,
						icon:"none"
					})
				})
				
				// 画指纹icon
				await this.$refs.rCanvas.drawImage({
					url:"/static/ljgd-icon.png",
					x:262,
					y:580,
					w:14,
					h:14
				}).catch(err_msg=>{
					uni.showToast({
						title:err_msg,
						icon:"none"
					})
				})
				
				// 精选好物icon
				await this.$refs.rCanvas.drawImage({
					url:"/static/jx-icon.png",
					x:20,
					y:580,
					w:14,
					h:14
				}).catch(err_msg=>{
					uni.showToast({
						title:err_msg,
						icon:"none"
					})
				})
				
				await this.$refs.rCanvas.drawImage({
					url:"/static/jdzg-icon.png",
					x:100,
					y:580,
					w:14,
					h:14
				}).catch(err_msg=>{
					uni.showToast({
						title:err_msg,
						icon:"none"
					})
				})
				
				
				await this.$refs.rCanvas.drawText({
					text:"京东价：",
					x:20,
					y:400,
					font_color:"white",
					font_size:12
				})
				
				await this.$refs.rCanvas.drawText({
					text:"原价:19999",
					x:352,
					y:430,
					line_through:true,
					font_color:"white",
					font_size:10,
					text_align:"right"
				})
				
				await this.$refs.rCanvas.drawText({
					text: "京东直供",
					max_width:0,
					x:118,
					y:590,
					font_color:"rgb(175, 174, 175)",
					font_size:11
				})
				
				await this.$refs.rCanvas.drawText({
					text:"精选好物",
					max_width:0,
					x:38,
					y:590,
					font_color:"rgb(175, 174, 175)",
					font_size:11
				})
				
				await this.$refs.rCanvas.drawText({
					text:"             膳魔师EHA/4101E/GM灰色饭煲套组210W送保温杯一个/好好好好好好好好好好好好好!!",
					max_width:210,
					line_height:20,
					x:20,
					y:490,
					font_color:"black",
					font_size:12
				})
				
				await this.$refs.rCanvas.drawText({
					text:"了解商品详情",
					max_width:0,
					x:280,
					y:590,
					font_color:"rgb(180, 180, 180)",
					font_size:11
				})
				
				await this.$refs.rCanvas.drawSpecialText([
					{
						text:"29999",
						x:20,
						y:430,
						font_color:"white",
						font_size:24
					},
					{
						text:"元",
						x:20,
						y:430,
						font_color:"white",
						font_size:12
					},
					{
						text:"+",
						x:20,
						y:430,
						font_color:"white",
						font_size:12
					},
					{
						text:"2000",
						x:20,
						y:430,
						font_color:"white",
						font_size:24
					},
					{
						text:"券",
						x:20,
						y:430,
						font_color:"white",
						font_size:12
					}
				])
				
				await this.$refs.rCanvas.fillRoundRect({
					x:20,
					y:476,
					w:38,
					h:18,
					radius:4,
					fill_color:"rgb(199, 21, 33)"
				})
				
				await this.$refs.rCanvas.drawText({
					text:"京东",
					x:27,
					y:490,
					font_color:"#fff",
					font_size:12
				})
				
				await this.$refs.rCanvas.draw((res)=>{
					//res.tempFilePath：生成成功，返回base64图片
					console.log("生成成功",res)
				})
			})
		}
	}
</script>