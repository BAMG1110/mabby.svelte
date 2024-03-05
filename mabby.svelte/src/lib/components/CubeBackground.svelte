<script>
import { onMount } from "svelte";
import * as THREE from "three";
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";

let container;
onMount(() => {
    let width = document.getElementById("bg").offsetWidth
    let height = document.getElementById("bg").offsetHeight
    let newFov = 130
    let fovdir = 1
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(40, width / height, 0.1, 1000);
    camera.position.set(0,0,15);
    
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(width, height);
    container.appendChild(renderer.domElement);
    
    const light1 = new THREE.PointLight(0x590098, 100, 100);
    light1.position.set(0, 0, 12);
    const light2 = new THREE.PointLight(0xfcd303, 100, 100);
    light2.position.set(0, 0, 3);
    scene.add(light1, light2);
    
    // const AmbientLight = new THREE.AmbientLight(0xffffff, 1, 100);
    // light.position.set(5, 5, 5);
    // scene.add(AmbientLight);
    
    const geometry = new THREE.BoxGeometry(10, 10, 10);
    const material = new THREE.MeshStandardMaterial();
    const cubesConfig = [
        { position: [0, -10, 0], scale: [1, 1, 1] }, // Piso
        { position: [0, 10, 0], scale: [1, 1, 1] }, // Techo
        { position: [10, 0, 0], scale: [1, 1, 1] }, // Pared derecha
        { position: [-10, 0, 0], scale: [1, 1, 1] }, // Pared izquierda
        { position: [0, 0, -10], scale: [1, 1, 1] } // Pared trasera
    ];

    for (let i = 0; i < cubesConfig.length; i++) {
        const cube = new THREE.Mesh(geometry, material);
        // Configurando la posición del cubo
        cube.position.set(...cubesConfig[i].position);
        // Configurando la escala del cubo
        cube.scale.set(...cubesConfig[i].scale);
        // Añadiendo el cubo a la escena
        scene.add(cube);
    }
    const loader = new GLTFLoader()
    loader.load('assets/Bee.glb', function(glft){
        glft.scene.scale.set(10, 10, 10)
        glft.scene.position.set(0,0,-4)
        scene.add(glft.scene)
    }, undefined, function(error){
        console.error(error)
    })

    const controls = new OrbitControls(camera, renderer.domElement);
    controls.update();

    const animate = function () {
        requestAnimationFrame(animate);
        controls.update();

        if (newFov > 130 || newFov < 10){
            fovdir *= -1
        }
        newFov = newFov + fovdir*0.01
        camera.fov = newFov;
        camera.updateProjectionMatrix();
        
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