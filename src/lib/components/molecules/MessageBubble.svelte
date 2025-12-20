<script>
  import Avatar from '../atoms/Avatar.svelte';

  export let role = 'user'; // 'user' | 'assistant'
  export let text = '';
  export let isTyping = false;

  function parseMarkdown(input) {
    if (!input) return '';
    
    // 1. Handle Bold (**text**)
    let processed = input.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
    
    // 2. Handle Bullet Lists (* item)
    const lines = processed.split('\n');
    let output = '';
    let inList = false;
    
    lines.forEach((line, index) => {
      const trimmed = line.trim();
      if (trimmed.startsWith('* ')) {
        if (!inList) {
          output += '<ul class="list-disc pl-6 my-2 space-y-1">';
          inList = true;
        }
        output += `<li>${trimmed.substring(2)}</li>`;
      } else {
        if (inList) {
          output += '</ul>';
          inList = false;
        }
        // Add <br> for newlines, but avoid extra breaks around lists if possible
        // For simplicity, we preserve the original line breaks structure
        if (index > 0) output += '<br>';
        output += line;
      }
    });
    
    if (inList) output += '</ul>';
    
    return output;
  }

  $: formattedText = parseMarkdown(text);
</script>

<div class="flex gap-[15px] max-w-full mb-5 {role === 'user' ? 'justify-end' : 'justify-start'}">
  {#if role === 'assistant'}
    <div class="shrink-0">
      <Avatar type="assistant" />
    </div>
  {/if}

  <div class="text-base leading-[1.6] max-w-[90%] md:max-w-[80%] break-words {role === 'user' ? 'bg-gemini-hover text-gemini-text rounded-[18px] rounded-br-[4px] p-[12px_18px]' : 'bg-transparent p-0 text-gemini-text w-full'} {isTyping ? 'italic text-[#8e918f] animate-pulse' : ''}">
    {#if role === 'user'}
      {text}
    {:else}
      {#if isTyping}
        Thinking...
      {:else}
        {@html formattedText}
      {/if}
    {/if}
  </div>
</div>
