
<script>
	import { Object3DInstance, useFrame, useThrelte } from 'threlte';
	import ThreeGlobe from 'three-globe';
    import * as d3 from 'd3';
    import  { displayData } from './data';

    export let hexdata;

    const colorAccessor = d => d.properties.GDP_MD_EST;
    const colorScale = d3.scaleSequential()
            .domain(d3.extent(hexdata, colorAccessor))
            .interpolator(d3.interpolateViridis);

    const yScale = d3.scaleLinear()
        .domain(d3.extent(hexdata, colorAccessor))
		.range([0, 8])
		.nice(true)        
   
    let globe = new ThreeGlobe()
      .globeImageUrl('./earth-dark.jpeg')
      .hexPolygonsData(hexdata)
      .hexPolygonResolution(4)
      .hexPolygonAltitude(d => yScale(colorAccessor(d)))
      .hexPolygonMargin(0.2)
      .hexPolygonColor( d => colorScale(colorAccessor(d)))
      

	useFrame(() => {
		globe = globe;
	});
	
</script>

<Object3DInstance object={globe} scale={0.02} castShadow receiveShadow/>

