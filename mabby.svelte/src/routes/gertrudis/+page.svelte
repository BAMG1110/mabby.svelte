<script>
    import { onMount } from 'svelte';
    import { GoogleGenerativeAI } from '@google/generative-ai';
    let text = "";
    let response = "";
    
    async function run() {
        const genAI = new GoogleGenerativeAI('AIzaSyCoqZ2J5oUPTu9XD1gaD4Ae04yEdz0Qt68');
        // For text-only input, use the gemini-pro model
        const model = genAI.getGenerativeModel({ model: "embedding-001"});

        const prompt = "Write a story about a magic backpack."

        const result = await model.generateContent(prompt);
        const response = await result.response;
        const text = response.text();
        console.log(text);
        return text
    }
</script>
  
<textarea bind:value={text} />
<button on:click={run}>Enviar</button>


<div class="child">
    <h1>gertrudis</h1>
    <div class="response">{response}</div>
</div>
