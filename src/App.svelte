<script>
  import { SphereBufferGeometry, MeshBasicMaterial, DoubleSide } from 'three';
  import { Canvas, PerspectiveCamera, AmbientLight, Mesh, OrbitControls } from 'threlte';
  import Hexglobe from "./lib/Hexglobe.svelte";

  let hexData;
  
  fetch('./countries.geo.json')
    .then((response) => response.json())
    .then((data) => {
      hexData = data.features;
    })
    .catch((error) => {
      console.log(error);
      return [];
    });
    
  </script>
  
  <div class="canvas-wrapper">
    <Canvas>
      <PerspectiveCamera fov={55} position={{ z: -25 }}>
        <OrbitControls autoRotate autoRotateSpeed={0.8} />
      </PerspectiveCamera>
      <AmbientLight intensity={0.9}  />
      
      <Mesh
        geometry={new SphereBufferGeometry()}
        material={new MeshBasicMaterial({ color: '#1F2022', side: DoubleSide })}
        scale={400}
      />
  
      {#if hexData}
        <Hexglobe hexdata={hexData}/>
      {/if}
    </Canvas>
  </div>
  
  <style>
    .canvas-wrapper {
      width: 100%;
      height: 100vh;
    }
  </style>