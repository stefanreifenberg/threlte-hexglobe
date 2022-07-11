
<script>
	import { Object3DInstance, useFrame } from 'threlte';
	import ThreeGlobe from 'three-globe';

    export let hexdata;
    
    let globe = new ThreeGlobe()
      .globeImageUrl('//unpkg.com/three-globe/example/img/earth-dark.jpg')
      .hexPolygonsData(hexdata)
      .hexPolygonResolution(3)
      .hexPolygonAltitude(0.001)
      .hexPolygonMargin(0.2)
      .hexPolygonColor(() => '#b5290d');

        
	useFrame(() => {
		globe = globe;
	});
	
</script>

<Object3DInstance object={globe} scale={0.07} />

