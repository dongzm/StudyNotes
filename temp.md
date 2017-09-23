```html
<style type="text/css">
	.btn_address{
	    display: inline-block;
    padding: 6px 12px;
    font-size: 14px;
    font-weight: 400;
    line-height: 1.42857143;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    touch-action: manipulation;
    cursor: pointer;
    user-select: none;
    background-image: none;
    border: 1px solid transparent;
    border-radius: 4px;
    color: #333;
    background-color: #fff;
    border-color: #ccc;
    margin-top: 5px;
    margin-bottom: 5px;
}
</style>
<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=51vOFPsInj6x27iz6whvjGaLbLLrT7He"></script>
<script type="text/javascript">
	// 百度地图API功能
	var addressArr = [{"address": "友德酒店", "lat": 24.903342, "lng": 118.616641 }, {"address": "泉州市大自然水疗养生休闲会所", "lat": 24.903342, "lng": 118.623849 }, {"address": "大自然水疗养生阳光会所", "lat": 24.818811, "lng": 118.596782 }, {"address": "大自然水疗养生休闲会所(晋江店)", "lat": 24.807755, "lng": 118.584008 }, {"address": "大自然水疗养生休闲会所(星光国际店)", "lat": 24.893678, "lng": 118.60863 }, {"address": "大自然水疗养生休闲会所(大红埔店)", "lat": 25.017923, "lng": 118.793759 }, {"address": "大自然水疗养生休闲会所(石狮店)", "lat": 24.743709, "lng": 118.62494 }]
	var lat, lng
	$(function(){
		initMap();
	})
	function initMap(){
		var map = new BMap.Map("allmap");
		var point = new BMap.Point(116.331398,39.897445);
		map.centerAndZoom(point,18);

		var geolocation = new BMap.Geolocation();
		geolocation.getCurrentPosition(function(r){
			if(this.getStatus() == BMAP_STATUS_SUCCESS){
				var mk = new BMap.Marker(r.point);
				map.addOverlay(mk);
				map.panTo(r.point);
				lng = r.point.lng
				lat = r.point.lat
				if (lng && lat) {
					$("#address").show();
				}
			}
			else {
				alert('failed'+this.getStatus());
			}        
		},{enableHighAccuracy: true})
	}
	function goto(index){
		if(lng && lat){
			var obj = addressArr[index];
			var url = "http://api.map.baidu.com/direction?origin=latlng:"+lat+","+lng+"|name:我的位置&destination=latlng:"+obj.lat+","+obj.lng+"|name:"+obj.address+"&mode=driving&region=西安&output=html&src=lcyx"
			window.location.href = url;
		}else{
			alert("当前位置获取失败，请刷新重试")
		}
	}
</script>
<div id="address" style="display: none;">
	<div id="allmap"></div>
	<div><button class="btn_address" onclick="goto(0)">友德酒店</button></div>
	<div><button class="btn_address" onclick="goto(1)">泉州市大自然水疗养生休闲会所</button></div>
	<div><button class="btn_address" onclick="goto(2)">大自然水疗养生阳光会所</button></div>
	<div><button class="btn_address" onclick="goto(3)">大自然水疗养生休闲会所(晋江店)</button></div>
	<div><button class="btn_address" onclick="goto(4)">大自然水疗养生休闲会所(星光国际店)</button></div>
	<div><button class="btn_address" onclick="goto(5)">大自然水疗养生休闲会所(大红埔店)</button></div>
	<div><button class="btn_address" onclick="goto(6)">大自然水疗养生休闲会所(石狮店)</button></div>
</div>
```
