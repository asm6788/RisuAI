<script lang="ts">
    import { CheckIcon } from "lucide-svelte";

    export let check = false
    export let onChange = (check:boolean) => {}
    export let margin = true
    export let name = ''
    export let hiddenName = false
    export let reverse = false
    export let className = ""
    export let grayText = false
</script>

<label 
    class={"flex items-center space-x-2 cursor-pointer" + (className ? " " + className : "") + (grayText ? " text-textcolor2" : " text-textcolor")}
    class:mr-2={margin}
    aria-describedby="{name} {check ? 'abled' : 'disabled'}"
    aria-labelledby="{name} {check ? 'abled' : 'disabled'}"
>
    {#if reverse}
        <span>{name}<slot /></span>
    {/if}
    <input 
        class="hidden" 
        type="checkbox" 
        alt={name}
        bind:checked={check}
        on:change={() => {
            onChange(check)
        }}
        aria-describedby="{name} {check ? 'abled' : 'disabled'}"
        aria-labelledby="{name} {check ? 'abled' : 'disabled'}"
    />
    <span 
        class="w-5 h-5 min-w-5 min-h-5 rounded-md border-2 border-darkborderc flex justify-center items-center {check ? 'bg-darkborderc' : 'bg-darkbutton'} transition-colors duration-200"
        aria-hidden="true"
        aria-describedby="{name} {check ? 'abled' : 'disabled'}"
        aria-labelledby="{name} {check ? 'abled' : 'disabled'}"
    >
        {#if check}
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="white" class="w-3 h-3" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
            </svg>
        {/if}
    </span>
    {#if !hiddenName && !reverse}
        <span>{name}<slot /></span>
    {/if}
</label>
