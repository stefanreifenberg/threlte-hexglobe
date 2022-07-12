
<script>
	import { Object3DInstance, useFrame } from 'threlte';
	import ThreeGlobe from 'three-globe';
    import * as d3 from 'd3';

    export let hexdata;
    const colorAccessor = d => d.properties.GDP_MD_EST;
    const colorScale = d3.scaleSequential()
            .domain(d3.extent(hexdata, colorAccessor))
            .interpolator(d3.interpolateViridis);
   
    let globe = new ThreeGlobe()
      .globeImageUrl('./earth-dark.jpeg')
      .hexPolygonsData(hexdata)
      .hexPolygonResolution(3)
      .hexPolygonAltitude(0.001)
      .hexPolygonMargin(0.2)
      .hexPolygonColor( d => colorScale(colorAccessor(d)))

	useFrame(() => {
		globe = globe;
	});
	
</script>

<Object3DInstance object={globe} scale={0.07} />

