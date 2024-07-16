<script lang="ts">
	import { browser } from '$app/environment';
	import {
		ArcRotateCamera,
		Color4,
		Engine,
		HemisphericLight,
		MeshBuilder,
		Scene,
		Vector3
	} from '@babylonjs/core';
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement | null = null;
	let engine: Engine | null = null;
	let scene: Scene | null = null;

	function resize() {
		engine?.resize();
	}

	function render() {
		scene?.render();
	}

	onMount(() => {
		engine = new Engine(canvas, true);
		scene = new Scene(engine);
		scene.clearColor = new Color4(0, 0.5, 1, 0.5);

		let camera = new ArcRotateCamera('cam', 0, Math.PI / 2, 5, Vector3.Zero(), scene);
		camera.setTarget(Vector3.Zero());

		camera.attachControl(canvas, true);
		let light = new HemisphericLight('light', Vector3.Down(), scene);
		light.intensity = 0.7;

		let box = MeshBuilder.CreateBox('box', { size: 1 }, scene);

		engine.runRenderLoop(render);
		if (browser) window.addEventListener('resize', resize);

		return () => {
			scene?.dispose();
			engine?.dispose();
			if (browser) window.removeEventListener('resize', resize);
		};
	});
</script>

<canvas bind:this={canvas}></canvas>

<style>
	canvas {
		width: 100%;
		height: 100%;
	}
</style>
