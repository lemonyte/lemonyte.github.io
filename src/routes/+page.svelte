<script lang="ts">
    import type { PageData } from "./$types";
    import Repository from "$lib/components/Repository.svelte";
    import IconLink from "$lib/components/IconLink.svelte";
    import Blob from "$lib/components/Blob.svelte";
    import { skills, links } from "$lib/data";

    const { data }: { data: PageData } = $props();
</script>

{#each Array(24) as _}
    <Blob spread={350} parallaxSensitivity={0.05} />
{/each}

<div class="flex justify-center text-neutral-800 dark:text-neutral-200 mb-10">
    <div class="w-screen flex flex-col gap-6">
        <div class="flex items-center flex-col">
            <div class="h-screen flex flex-col justify-center">
                <h1 class="text-7xl sm:text-8xl md:text-9xl select-none">Lemonyte</h1>
            </div>
            <div
                class="flex flex-shrink-0 gap-4 text-neutral-700 dark:text-neutral-300 backdrop-blur-3xl p-4 rounded-xl bg-neutral-100 dark:bg-neutral-900 !bg-opacity-40"
            >
                {#each links as link}
                    <IconLink {...link} />
                {/each}
            </div>
        </div>
        <div class="flex flex-col items-center w-full">
            <div
                class="w-11/12 md:w-2/3 p-6 backdrop-blur-3xl rounded-xl bg-neutral-100 dark:bg-neutral-900 !bg-opacity-40"
            >
                <p>
                    Hi, I'm <strong>Lemonyte</strong>, an open-sourcerer 🧙‍♂️ passionate about the world of software and
                    technology.
                </p>
                <ul class="p-4 list-disc">
                    <li>
                        ❤️ I love
                        <a href="https://github.com/lemonyte/terminal-player">terminals</a>
                        and making things that are
                        <a href="https://github.com/lemonyte/ferry-planner">useful</a>
                        to others.
                    </li>
                    <li>
                        🧠 I'm always trying to expand my knowledge and skillset, so I'm learning Rust 🦀 right now.
                    </li>
                    <li>
                        💡 I like to learn about anything that sparks my interest, like
                        <a href="https://github.com/lemonyte/wastebin">web development</a>,
                        <a href="https://github.com/lemonyte/pyautotrace">image vectorization</a>,
                        <a href="https://github.com/lemonyte/russian-roulette-bot">Discord bots</a>, and
                        <a href="https://github.com/lemonyte/stegosaurus">cryptography</a>.
                    </li>
                    <li>
                        🔥 I believe in writing structured, readable, maintainable code, and occasionally having some
                        <a href="https://github.com/lemonyte/http-waifus">fun</a>.
                    </li>
                    <li>
                        🤝 I'm quite
                        <a href="https://liberamanifesto.com">fond of open source</a>
                        and I'm always looking for ways to contribute and give back.
                    </li>
                    <li>
                        💭 I'm dreaming of a future where software and hardware exist in the hands of the people, for
                        the people, and by the people, without technological limitations.
                    </li>
                </ul>
            </div>
        </div>
        <div class="flex flex-col items-center">
            <div
                class="w-11/12 md:w-2/3 p-6 backdrop-blur-3xl rounded-xl bg-neutral-100 dark:bg-neutral-900 !bg-opacity-40"
            >
                <h2 class="text-2xl mb-4">Skills</h2>
                <div class="grid grid-cols-[repeat(auto-fit,_minmax(40px,_1fr))] gap-1">
                    {#each skills as skill}
                        <IconLink {...skill} />
                    {/each}
                </div>
            </div>
        </div>
        <div class="flex flex-col items-center">
            <div
                class="w-11/12 md:w-2/3 p-6 backdrop-blur-3xl rounded-xl bg-neutral-100 dark:bg-neutral-900 !bg-opacity-40"
            >
                <h2 class="text-2xl mb-4">Projects</h2>
                <div class="grid grid-cols-1 gap-2 md:grid-cols-2">
                    {#await data.reposResponse}
                        {#each Array(6) as _}
                            <Repository />
                        {/each}
                    {:then repos}
                        {#await repos.json() then repos}
                            {#each repos as repo}
                                <Repository {...repo} />
                            {/each}
                        {:catch error}
                            <pre class="text-red-500">{error.message}</pre>
                        {/await}
                    {:catch error}
                        <pre class="text-red-500">{error.message}</pre>
                    {/await}
                </div>
            </div>
        </div>
    </div>
</div>

<style lang="postcss">
    a {
        @apply transition text-sky-700 dark:text-sky-500 hover:underline hover:brightness-150 dark:hover:brightness-75;
    }

    li {
        @apply my-1;
    }
</style>
