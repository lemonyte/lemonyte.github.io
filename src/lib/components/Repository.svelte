<script lang="ts">
    export let repo = "";
    export let link = "";
    export let description = "";
    export let language = "";
</script>

<a
    href={link}
    class="p-3 rounded-lg transition ease-in duration-100 select-none bg-neutral-100 hover:bg-neutral-200 dark:bg-neutral-900 dark:hover:bg-neutral-800"
>
    <div class="justify-between flex flex-row">
        <div
            class="text-xl overflow-hidden text-ellipsis whitespace-nowrap"
            class:animate-pulse={!repo}
        >
            {repo || "Loading…"}
        </div>
        {#if language}
            <div class="p-1 text-xs rounded-md items-center flex bg-neutral-300 dark:bg-neutral-700">
                {language}
            </div>
        {/if}
    </div>
    <div class="text-neutral-500 text-sm text-ellipsis truncate" class:animate-pulse={!repo}>
        {description || "Loading..."}
    </div>
</a>
