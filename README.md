### r-canvas简介
插件名：r-canvas</br>
插件说明：基于原生canvas绘制2D海报，canvas原生方法的二次封装，生成图片不失帧！

### r-canvas兼容性
此插件适应所有手机屏幕，也适用于ios、android、微信小程序、h5等平台（已经过测试），其它端还请开发者们自行测试，因为是基于canvas原生函数的二次封装，所以其他端应该正常能用（其它端能否使用欢迎留言反馈）！

### r-canvas示例
码云地址：[https://gitee.com/citn/r-canvas-example](https://gitee.com/citn/r-canvas-example)</br>
github地址：[https://github.com/MyL2H/r-canvas-example](https://github.com/MyL2H/r-canvas-example)

### r-canvas借助第三方插件
r-canvas解决了画图片的兼容性，支持的图片路径有：</br>
1、本地图片路径（示例：“/static/ercode.png”）</br>
2、网络路径（需要支持跨域的图片路径）</br>
3、base64</br>
由于本地图片需要借助 [image-tools](https://ext.dcloud.net.cn/plugin?id=123) 把本地图片转成base64，所以此插件包含了 [image-tools](https://ext.dcloud.net.cn/plugin?id=123) 插件的代码！非常感谢此插件的作者！

### 使用方式

在template中引入组件
```html
<r-canvas ref="rCanvas"></r-canvas>
```
</br>

在script中引入组件
```javascript
import rCanvas from "@/components/r-canvas/r-canvas.vue"
export default{
	components:{
		rCanvas
	}
}
```

### 使用示例
```javascript
onLoad(){
	this.$nextTick(async ()=>{
		// 初始化
		await this.$refs.rCanvas.init({
			canvas_id:"rCanvas"
		})
		
		// 画图
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
		
		// 画文字
		await this.$refs.rCanvas.drawText({
			text:"精选好物",
			max_width:0,
			x:38,
			y:590,
			font_color:"rgb(175, 174, 175)",
			font_size:11
		})
		
		// 生成海报
		await this.$refs.rCanvas.draw((res)=>{
			//res.tempFilePath：生成成功，返回base64图片
		})
	})
}
```

### 方法说明
|  方法名称   | 说明  | 成功回调 | 失败回调
|  :----  | :----  |  :----  | :----  |
| init  | 初始化canvas | .then() | .catch()
| drawImage  | 画图 | .then() | .catch()
| drawText  | 画文字 | .then() | .catch()
| drawSpecialText  | 画多样性文字 | .then() | .catch()
| fillRoundRect  | 画圆角矩形 | .then() | .catch()
| draw  | 生成海报 | .then() | .catch()

每个方法都有成功回调.then() 和 .catch(),.catch()会有错误信息返回，建议写上.catch()

#### init方法说明
|  属性名   |  默认值 | 类型 | 是否必填 | 说明
|  :----   |  :----  | :----  | :----  |  :----  |
| canvas_id  |  | String | 是 | id唯一 |
| canvas_width  | uni.getSystemInfoSync().windowWidth | Number | 否 | 画布宽度，不填则默认设备屏幕宽度 | 
| canvas_height  | uni.getSystemInfoSync().windowHeight | Number | 否 | 画布高度，不填则默认设备屏幕高度 | 
| background_color  | #ffffff | String |  否 | 画布颜色 |
| hidden  | false | Boolean |  否 | 是否隐藏画布不呈现在页面上 |

#### drawImage方法说明
|  属性名   | 默认值 | 类型 | 是否必填 | 说明
|  :----  | :----  |  :----  | :----  | :----  |
| url  |   | String | 是 | 支持本地图片、网络路径（需支持跨域）、baes64 |
| x    |   | Number | 是 | 图片横坐标 | 
| y    |   | Number | 是 | 图片纵坐标 | 
| w    |   | Number | 是 | 图片宽度 | 
| h    |   | Number | 是 | 图片高度 | 

#### drawText方法说明
|  属性名   | 默认值 | 类型 | 是否必填 | 说明
|  :----  | :----  |  :----  | :----  | :----  |
| text | | String | 是 | 文字内容
| x | | Number | 是 | 文字横坐标 |
| y | | Number | 是 | 文字纵坐标 |
| font_color | #000 |  String | 否 | 文字颜色 |
| font_size | 20 | Number | 否 | 文字大小 |
| font_family | Arial | String | 否 | 文字字体
| text_align | left | String | 否 | 文字对齐方式</br>left:居左</br>center:居中</br>right:居右
| line_through | false | Boolean | 否 | 是否给文字添加中划线
| max_width |  | Number | 否 | 文字到达最大宽度，会自动换行
| line_height | 20 | Number | 否 | 文字行高，设置max_width属性才能生效

#### drawSpecialText方法说明
|  属性名   | 默认值 | 类型 | 是否必填 | 说明
|  :----  | :----  |  :----  | :----  | :----  |
| [] | | Array | 是 | 数组

**数组字段说明**

|  属性名   | 默认值 | 类型 | 是否必填 | 说明
|  :----  | :----  |  :----  | :----  | :----  |
| text | | String | 是 | 文字内容
| x | | Number | 是 | 文字横坐标 |
| y | | Number | 是 | 文字纵坐标 |
| font_color | #000 |  String | 否 | 文字颜色 |
| font_size | 20 | Number | 否 | 文字大小 |
| font_family | Arial | String | 否 | 文字字体


#### fillRoundRect方法说明
|  属性名   | 默认值 | 类型 | 是否必填 | 说明
|  :----  | :----  |  :----  | :----  | :----  |
| x | | Number | 是 | 矩形横坐标 |
| y | | Number | 是 | 矩形纵坐标 |
| w | | Number | 是 | 矩形宽度 | 
| h | | Number | 是 | 矩形高度 | 
| radius | | Number | 是 | 矩形圆角弧度 | 
| fill_color | | String | 是 | 矩形颜色 | 

#### draw方法说明
|  属性名   | 默认值 | 类型 | 是否必填 | 说明
|  :----  | :----  |  :----  | :----  | :----  |
| callback | | Function | 否 | 成功回调callback，也可以用.then获取成功回调 |

</br>
</br>

### 学习交流微信
![交流微信](http://www.xvue.cn/rohlin-wechat-ercode.jpg)
