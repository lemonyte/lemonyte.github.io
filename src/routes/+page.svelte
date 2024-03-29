<script lang="ts">
    import { blur } from "svelte/transition";
    import Repository from "$lib/components/Repository.svelte";
    import Link from "$lib/components/Link.svelte";
    import { skills, links } from "$lib/data";

    export let data;
    const { repos } = data;
</script>

<div class="m-6 flex justify-center text-neutral-800 dark:text-neutral-200" in:blur={{ duration: 1000 }}>
    <div class="md:w-1/2 flex flex-col gap-6">
        <div class="flex items-center">
            <h1 class="text-4xl flex-grow">Lemonyte</h1>
            <div class="flex flex-shrink-0 gap-4 text-neutral-700 dark:text-neutral-300">
                {#each links as link}
                    <Link {...link} />
                {/each}
            </div>
        </div>
        <div>
            <p>
                Hello fellow traveller! I'm <strong>Lemonyte</strong>, an open-sourcerer 🧙‍♂️ passionate about the world
                of software and technology.
            </p>
            <ul class="p-4 list-disc">
                <li>
                    ❤️ I love <a href="https://github.com/lemonyte/terminal-player">terminals</a> and making things
                    that are <a href="https://github.com/lemonyte/ferry-planner">useful</a> to others.
                </li>
                <li>🧠 I'm always trying to expand my knowledge and skillset, so I'm learning Rust right now.</li>
                <li>
                    💡 I like to learn about anything that sparks my interest, like <a
                        href="https://github.com/lemonyte/wastebin">web development</a
                    >, <a href="https://github.com/lemonyte/pyautotrace">image vectorization</a>,
                    <a href="https://github.com/lemonyte/russian-roulette-bot">Discord bots</a>, and
                    <a href="https://github.com/lemonyte/stegosaurus">cryptography</a>.
                </li>
                <li>
                    🔥 I believe in writing structured, readable, maintainable code, and occasionally having some <a
                        href="https://github.com/lemonyte/http-waifus">fun</a
                    >.
                </li>
                <li>
                    🤝 I'm quite <a href="https://liberamanifesto.com">fond of open source</a> and I'm always looking for
                    ways to contribute and give back.
                </li>
                <li>
                    💭 I'm dreaming of a future where software and hardware exist in the hands of the people, for the
                    people, and by the people, without technological limitations.
                </li>
            </ul>
        </div>
        <div class="grid grid-cols-1 gap-2 md:grid-cols-2">
            {#await repos.json()}
                {#each Array(6) as _}
                    <Repository />
                {/each}
            {:then repos}
                {#each repos as repo}
                    <Repository {...repo} />
                {/each}
            {:catch error}
                <pre class="text-red-500">{error.message}</pre>
            {/await}
        </div>
        <div>
            <h2 class="text-2xl mb-4">Skills</h2>
            <div class="grid grid-cols-[repeat(auto-fit,_minmax(40px,_1fr))] gap-1">
                {#each skills as skill}
                    <Link {...skill} />
                {/each}
            </div>
        </div>
    </div>
</div>

<style lang="postcss">
    a {
        @apply transition text-sky-500;
    }

    a:hover {
        @apply brightness-75;
    }

    li {
        @apply my-1;
    }
</style>
