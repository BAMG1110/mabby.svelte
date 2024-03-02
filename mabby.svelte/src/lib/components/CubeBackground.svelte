<script>
import { onMount } from "svelte";
import * as THREE from "three";
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";

let container;
onMount(() => {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(120, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0,0,10);
    
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    container.appendChild(renderer.domElement);
    
    const light = new THREE.PointLight(0xffffff, 100, 100);
    light.position.set(0, 0, 5);
    scene.add(light);
    
    const AmbientLight = new THREE.AmbientLight(0xffffff, 1, 100);
    light.position.set(5, 5, 5);
    scene.add(AmbientLight);
    
    const geometry = new THREE.BoxGeometry(10, 10, 10);
    const material = new THREE.MeshStandardMaterial();
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);
    
    // const loader = new GLTFLoader()
    // loader.load('assets/interogation_room.glb', function(glft){
    //     scene.add(glft.scene)
    // }, undefined, function(error){
    //     console.error(error)
    // })

    // const controls = new OrbitControls(camera, renderer.domElement);
    // controls.update();

    const animate = function () {
        requestAnimationFrame(animate);
        // controls.update();
        
        renderer.render(scene, camera);
    };

    animate();

    window.addEventListener('resize', () => {
        let width = document.getElementById("bg").offsetWidth
        let height = document.getElementById("bg").offsetHeight
        camera.aspect = width / height;
        // cube.scale(width/2, height/2, 1)
        camera.updateProjectionMatrix();
        renderer.setSize(width, height);
    });
});
</script>

<style>
.scene {
  z-index: 0;
  grid-area: 1 / 1 / -1 / -1;
}
</style>

<div class="scene" bind:this={container}></div>