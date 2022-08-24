<script lang="ts">
	import { onMount } from 'svelte';
	import * as Cesium from 'cesium';
	import '../node_modules/cesium/Build/Cesium/Widgets/widgets.css'

	window['CESIUM_BASE_URL'] = './build';

  let viewer: Cesium.Viewer;
	Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIzYTkzMzFkMC05ZDYwLTRlNDEtODJmNi1kOTRlOTc0ZGRkYmMiLCJpZCI6Mjc4MjcsInNjb3BlcyI6WyJhc2wiLCJhc3IiLCJhc3ciLCJnYyIsInByIl0sImlhdCI6MTU5MDEzMDg4OX0.mdLKBX5lSAtGUcioB8nkVnnORU1Lsn44rLe3eF6nrio';

	onMount(() => {
		viewer = new Cesium.Viewer('cesiumContainer',{
			orderIndependentTranslucency: false,
			contextOptions: {
					webgl: {
							alpha: true,
					}
			},
			geocoder:false,//搜索功能
			homeButton:false,//视角恢复功能
			sceneModePicker:false,// 2d、3d切换功能
			baseLayerPicker:false,//地图底色选择功能
			navigationHelpButton:false,//帮助功能
			animation:false,//动画功能
			creditcontainer: "credit",//关闭数据来源
			timeline:false,//时间线功能
			fullscreenButton:false //全屏功能
		});
		viewer.scene.skyBox.show = false;
		viewer.scene.backgroundColor = new Cesium.Color(0.0, 0.0, 0.0, 0.0);
		//隐藏太阳
		viewer. scene.globe.enableLighting = false;viewer.shadows = false;
		viewer.scene.sun. show=false;//还可以viewer. scene.sun. destroy ();//月亮
		viewer. scene.moon.show=false;//大气
		viewer. scene.skyAtmosphere.show=false;//雾
		viewer.scene.fog.enable=false;
	});
</script>

<main>
	<!-- <div data-tauri-drag-region class="container">
		<div data-tauri-drag-region class="box">
			<div data-tauri-drag-region class="box-panel"></div>
			<div data-tauri-drag-region class="box-panel"></div>
			<div data-tauri-drag-region class="box-panel"></div>
			<div data-tauri-drag-region class="box-panel"></div>
			<div data-tauri-drag-region class="box-panel"></div>
			<div data-tauri-drag-region class="box-panel"></div>
		</div>
	</div> -->
	<div data-tauri-drag-region class="mask"></div>
	<div id="cesiumContainer"></div>
</main>

<style>
	:global(body) {
		padding: 0;
		margin: 0;
		user-select: none;
	}

	:global(.cesium-viewer-bottom){
		display: none !important;
	}

	main {
		width: 100%;
    height: 100%;
	}

	.mask{
		position: absolute;
		top: 95%;
    left: 95%;
		width: 10px;
		height: 10px;
		z-index: 10;
		border-radius: 50%;
		background-color: white;
		cursor: move;
	}

	#cesiumContainer {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    overflow: hidden;
	}

	/* .container {
		flex: 1 1;
		transform: translate(90px,90px);
	}

	.box {
		transform-style: preserve-3d;
		transform-origin: 60px 60px;
    perspective-origin: center;
		animation-name: animation;
		animation-timing-function: ease-in-out;
		animation-iteration-count: infinite;
		animation-duration: 3s;
	}

	.box-panel {
		width: 120px;
		height: 120px;
		position: absolute;
		background-color: #337eee60;
	}

	.box-panel:nth-child(1) {
		transform: translateZ(60px);
	}
	.box-panel:nth-child(2) {
		transform: translateZ(-60px);
	}
	.box-panel:nth-child(3) {
		transform: rotateX(90deg) translateZ(60px);
	}
	.box-panel:nth-child(4) {
		transform: rotateX(-90deg) translateZ(60px);
	}
	.box-panel:nth-child(5) {
		transform: rotateY(90deg) translateZ(-60px);
	}
	.box-panel:nth-child(6) {
		transform: rotateY(90deg) translateZ(-60px);
	}

	@keyframes animation {
		16%{transform: rotateY(-90deg)}
		33%{transform: rotateY(-90deg) rotateZ(135deg)}
		50%{transform: rotateY(225deg) rotateZ(135deg)}
		66%{transform: rotateY(135deg) rotateZ(135deg)}
		83%{transform: rotateX(135deg)}
	} */
</style>