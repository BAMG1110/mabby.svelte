<script>
    import { onMount } from "svelte";
    import * as THREE from "three";
    import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
    import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";
    
    let container;

    
    
    onMount(() => {
        // static data
        const chunkSize = 16
        const chunk = new Uint8Array(chunkSize*chunkSize*chunkSize)

        // settings
        let width = document.getElementById("bg").offsetWidth
        let height = document.getElementById("bg").offsetHeight
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(40, width / height, 0.1, 1000);
        camera.position.set(0,0,40);
        
        const renderer = new THREE.WebGLRenderer();
        renderer.setSize(width, height);
        container.appendChild(renderer.domElement);

        const AmbientLight = new THREE.AmbientLight(0xffffff, 1, 100);
        scene.add(AmbientLight);
        
        // assets
        const geometry = new THREE.BoxGeometry(1,1,1)
        const material = new THREE.MeshPhongMaterial({color: 'red'})

        for(let y = 0-(chunkSize/2); y<chunkSize/2; ++y){
            for(let z = 0-(chunkSize/2); z<chunkSize/2; ++z){
                for(let x = 0-(chunkSize/2); x<chunkSize/2; ++x){
                    const offset = y*chunkSize*chunkSize + z*chunkSize + x
                    const voxel = chunk[offset]

                    // render optimization
                    // create mesh
                    const mesh = new THREE.Mesh(geometry, material)
                    mesh.position.set(x, y, z)
                    scene.add(mesh)
                }
            }
        }
    
        // helpers
        const controls = new OrbitControls(camera, renderer.domElement);
        controls.update();
    
        // game loop
        const animate = function () {
            requestAnimationFrame(animate);
            controls.update();
            camera.updateProjectionMatrix();
            
            renderer.render(scene, camera);
        };
    
        animate();
    
        window.addEventListener('resize', () => {
            let width = document.getElementById("bg").offsetWidth
            let height = document.getElementById("bg").offsetHeight
            camera.aspect = width / height;
            camera.updateProjectionMatrix();
            renderer.setSize(width, height);
        });
    });
</script>
    
<div class="scene" bind:this={container}></div>

<style>
    .scene {
    z-index: 0;
    grid-area: 1 / 1 / -1 / -1;
    }
</style>
    