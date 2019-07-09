<template>
	<div id="app">
		<div id="main" style="width: 900px; height:600px;"></div>
	</div>
</template>

<script>
	import HelloWorld from './components/HelloWorld.vue'

	export default {
		name: 'app',
		components: {
			HelloWorld
		},
		mounted() { // 执行在钩子函数当中

			// 得到包中的ECharts
			var echarts = require('echarts');

			// 基于准备好的dom，初始化echarts实例
			var myChart = echarts.init(document.getElementById('main'));

			// 事先准备好的图片
			let rankingIcons = {
				'one': require('./assets/1.png'),
				'two': require('./assets/2.png'),
				'three': require('./assets/3.png'),
				'four': require('./assets/4.png'),
				'five': require('./assets/5.png'),
				'six': require('./assets/6.png'),
				'seven': require('./assets/7.png'),
				'eight': require('./assets/8.png'),
				'nine': require('./assets/9.png'),
				'ten': require('./assets/10.png'),
			};

			// ECharts的配置项
			var option = {
				title: { // 设置图表标题
					text: 'Top10',
					textStyle: {
						fontWeight: "bold",
						color: "red"
					},
				},
				tooltip: { // 设置鼠标悬停显示效果
					trigger: 'axis',
					axisPointer: {
						type: 'cross', // 设置鼠标的悬停效果为显示横纵轴数据
					},
					formatter: function (params) { // 自定义显示格式
						// 自定义提示框
						var result = '';
						result += `<span style="display:inline-block; position:absolute; left:5px">${params[0].axisValue}</span>` + "</br>"
						// 自定义提示框，小点添加
						let marker = `<span style="display:inline-block; margin-right:5px; border-radius:10px; width:10px; height:10px; background-color:rgb(40,210,240);"></span>`
						result += marker + "金额: " + params[0].value;
						return result;
					}
				},
				grid: {
					left: '3%',
					right: '4%',
					bottom: '3%',
					containLabel: true // 显示标签名称
				},
				xAxis: [{
					show: false, // 不显示X轴
				}],
				yAxis: {
					type: 'category',
					axisLine: { show: false }, // 不显示Y轴竖线
					axisTick: { show: false }, // 不显示Y轴坐标
					data: ['缪超', '薛佳运', '刘庆智', '董洋', '孔德娜', '刘敏', '孟蕾', '朱沛冉', '杨涤非', '李竞'],
					axisLabel: {
						formatter: function (value, index) {
							let mapping = {
								1: 'one',
								2: 'two',
								3: 'three',
								4: 'four',
								5: 'five',
								6: 'six',
								7: 'seven',
								8: 'eight',
								9: 'nine',
								10: 'ten',
							}
							return '{value|' + value + '}   {' + mapping[10 - index] + '|}';
						},
						margin: 20,
						rich: {
							value: {
								lineHeight: 30,
								align: 'center'
							},
							one: {
								height: 23,
								lineHeight: 23,
								width: 23,
								backgroundColor: {
									image: rankingIcons.one
								}
							},
							two: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.two
								}
							},
							three: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.three
								}
							},
							four: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.four
								}
							},
							five: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.five
								}
							},
							six: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.six
								}
							},
							seven: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.seven
								}
							},
							eight: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.eight
								}
							},
							nine: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.nine
								}
							},
							ten: {
								height: 23,
								width: 23,
								lineHeight: 23,
								backgroundColor: {
									image: rankingIcons.ten
								}
							}
						} // rich
					}, // axisLabel
				}, // yAxis
				series: [
					{ // 设置柱状图样式
						type: 'bar',
						barGap: '-60%', // 设置柱间距离
						data: [1000000, 2000000, 3000000, 4000000, 5000000, 8000000, 12000000, 17000000, 45000000, 50000000],
						itemStyle: {
							normal: {
								borderWidth: 1,
								borderColor: 'rgb(99,195,228)',
								barBorderRadius: [40, 40, 40, 40], // 设置成圆角矩形
								color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [{ // 分别是左、下、右、上
									offset: 0,
									color: "rgb(47,207,234)" // 0% 处的颜色
								}, {
									offset: 1,
									color: "rgb(82,212,167)" // 100% 处的颜色
								}], false)
							} // normal
						} // itemStyle
					}, // 设置柱状图样式
					{ // 设置柱状图背景槽样式
						type: 'bar',
						barGap: '-100%',
						data: [50000000, 50000000, 50000000, 50000000, 50000000, 50000000, 50000000, 50000000, 50000000, 50000000],
						itemStyle: {
							normal: {
								borderWidth: 1,
								borderColor: 'rgb(99,195,228)',
								barBorderRadius: [40, 40, 40, 40], // 设置成圆角矩形
								color: new echarts.graphic.LinearGradient(1, 1, 1, 1, [{ // 分别是左、下、右、上
									offset: 0,
									color: "#fff" // 0% 处的颜色
								}, {
									offset: 1,
									color: "#fff" // 100% 处的颜色
								}], false)
							} // normal
						} // itemStyle
					} // 设置柱状图背景槽样式
				] // series
			}; // option

			// 使用刚指定的配置项和数据显示图表。
			myChart.setOption(option);
		}
	}
</script>

<style>
	
</style>