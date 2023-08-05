<svelte:head>
</svelte:head>

<script>
    import {onMount} from 'svelte';
    import * as THREE from 'three';

    /** @type {HTMLCanvasElement} */
    let canvas;

    onMount(() => {
        const renderer = new THREE.WebGLRenderer({antialias: true, canvas});

        const fov = 75;
        const aspect = 2;
        const near = 0.1;
        const far = 5;
        const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
        camera.position.z = 2;

        const scene = new THREE.Scene();
        const boxW = 1;
        const boxH = 1;
        const boxD = 1;
        const geometry = new THREE.BoxGeometry(boxW, boxH, boxD);
        const material = new THREE.MeshBasicMaterial({color: 0x44aa88});
        const cube = new THREE.Mesh(geometry, material);
        scene.add(cube);
        let time = new Date().getMilliseconds();
        function render(time) {
            time *= 0.001; //convert time to secs
            
            cube.rotation.x = time;
            cube.rotation.y = time;

            renderer.render(scene, camera);

            requestAnimationFrame(render);
        }
        requestAnimationFrame(render);
    })
</script>

<style>
    :global(*) {
        padding: 0;
        margin: 0;
    }
    
    .main{
        width: 100vw;
        height: 100vh;
    }
</style>

<div class="main">
    <canvas bind:this={canvas}></canvas>
</div>