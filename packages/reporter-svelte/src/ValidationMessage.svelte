<script>
  import { getContext, onMount } from 'svelte';
  import { formKey } from './key';
  import { getPath, isFormControl, _get } from '@felte/common';
  let errorFor;
  export { errorFor as for };
  const errors = getContext(formKey);
  let errorPath;
  onMount(() => {
    const control = document.getElementById(errorFor);
    if (!control || !isFormControl(control)) return;
    errorPath = getPath(control);
  });
  $: messages = errorPath && _get($errors, errorPath)
</script>

{#if errorPath && (messages || !$$slots.placeholder)}
  <slot {messages}></slot>
{:else if errorPath}
  <slot name="placeholder"></slot>
{/if}
