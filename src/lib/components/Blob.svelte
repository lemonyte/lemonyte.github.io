<script lang="ts">
    import { onMount } from "svelte";

    export let spread = 250;
    export let parallaxSensitivity = 0.05;

    let clientWidth: number;
    let clientHeight: number;
    let offsetX: number;
    let offsetY: number;
    const offsetZ = Math.random();
    const styles = {
        left: "",
        top: "",
        "--breathe-speed": `${5 + Math.floor(Math.random() * 15)}s`,
        "background-color": "black",
    };

    onMount(() => {
        offsetX = Math.floor(clientWidth / 2 + spread * (Math.random() - 0.5) * 2);
        offsetY = Math.floor(clientHeight / 2 + spread * (Math.random() - 0.5) * 2);
        styles.left = `calc(50vw - ${offsetX}px)`;
        styles.top = `calc(50vh - ${offsetY}px)`;
        styles["background-color"] =
            `rgb(${Math.floor(Math.random() * 127)}, ${Math.floor(Math.random() * 255)}, 255)`;
    });

    const parallax = (event: MouseEvent) => {
        const center = {
            x: window.innerWidth / 2,
            y: window.innerHeight / 2,
        };
        const mouseOffset = {
            x: (event.clientX - center.x) * parallaxSensitivity * offsetZ,
            y: (event.clientY - center.y) * parallaxSensitivity * offsetZ,
        };
        styles.left = `calc(50vw - ${offsetX + mouseOffset.x}px)`;
        styles.top = `calc(50vh - ${offsetY + mouseOffset.y}px)`;
    };
</script>

<svelte:window on:mousemove={parallax} />

<div
    bind:clientWidth
    bind:clientHeight
    class="bg-blob"
    style:left={styles.left}
    style:top={styles.top}
    style:--breathe-speed={styles["--breathe-speed"]}
    style:background-color={styles["background-color"]}
    role="none"
></div>

<style lang="postcss">
    @keyframes breathe {
        0% {
            opacity: 0.2;
        }
        100% {
            opacity: 0.4;
        }
    }

    @keyframes rotate {
        0% {
            offset-distance: 0%;
        }
        100% {
            offset-distance: 100%;
        }
    }

    .bg-blob {
        @apply blur-3xl;
        /* This forces the blob's position to the center of the page. */
        /* offset-path: circle(5%); */
        position: fixed;
        width: 20vh;
        height: 20vh;
        animation:
            var(--breathe-speed) ease-in-out infinite alternate breathe,
            60s linear infinite rotate;
        transition: background-color 10s;
        z-index: -30;
        left: 40vw;
        top: 40vh;
        background-color: black;
    }
</style>
