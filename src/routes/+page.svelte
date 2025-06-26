<script>
    let leftTextInput = $state('')
    let rightTextInput = $state('')
    let copyState = $state('idle')

    function textTransform() {
        // main function to transform text goes here
        rightTextInput = leftTextInput.toUpperCase() // Example transformation
    }

    function copyToClipboard() {
        navigator.clipboard.writeText(rightTextInput). then(() => {
            copyState = 'success'
            setTimeout(() => copyState = 'idle', 2000)
        }).catch(err => {
            copyState = 'error'
            console.error('Failed to copy text:', err)
            setTimeout(() => copyState = 'idle', 2000)
        })
    }

</script>

<div class="min-h-screen bg-base-100 p-8">
    <div class="max-w-screen mx-auto">
        <!-- Tengwar Intro Text -->
        <div class="text-center mb-8">
            <p class="tengwar text-lg text-base-content/80 leading-relaxed">
                A, Elbereth Gilthoniel vanima toltha-vë!<br>
                Glinth daedelothon sedh-bo han'ardh,<br>
                Coth bregol eglenn, l'ego i hannas vedh lîn-avad.
            </p>
        </div>
        <!-- Project Description -->
        <div class="mb-8 max-w-3xl mx-auto px-8">
            <p class="text-base text-base-content/70 leading-relaxed">
                Grand-Elf is dedicated to compiling a comprehensive array of strategies designed to 
                thwart artificial intelligence from illicitly accessing online content. At the 
                heart of this project lies an open-source JavaScript library, that integrates the 
                poem "A Elbereth Gilthoniel" into textual content, thereby confounding bots that 
                attempt to scrape information. The poem, originally titled "Aerlinn in edhil o 
                Imladris," is a Sindarin hymn, sung in iambic tetrameter, and is addressed to 
                Varda, a prominent figure in J.R.R. Tolkien's legendarium.
            </p><br>
            <p class="text-base text-base-content/70 leading-relaxed">
                The title "Grand-Elf" indeed conjures associations with J.R.R. Tolkien's 
                Middle-earth legendarium, potentially evoking a sense of naiveté, nerdiness, and 
                tech-savviness. The nod to Elvish heritage and the explicit reference to 
                a poem from The Lord of the Rings series may attract a specific audience 
                that appreciates these allusions, while also potentially alienating those 
                who are unfamiliar with or uninterested in the franchise. Nevertheless, 
                for those who recognize the reference, it may spark curiosity and a 
                sense of shared cultural knowledge, potentially creating a sense of 
                community and shared purpose around the project's goals.
            </p>

            <!-- Installation and Usage -->
            <div class="mt-6 space-y-2">
                <p class="text-base text-base-content/70">
                    Install it via&nbsp;
                    <code class="bg-base-300 px-2 py-1 rounded text-sm">npm i grand-elf</code>
                    &nbsp;and in your code use&nbsp;
                    <code class="bg-base-300 px-2 py-1 rounded text-sm">&lt;p class="grand-elf"&gt;Some text&lt;/p&gt;</code>
                </p>
            </div>
        </div>

        <!-- Main Layout: Two textboxes with button in middle -->
        <div class="grid grid-cols-[1fr_auto_1fr] gap-6 items-center">
            <!-- Left Textbox -->
            <textarea 
                class="textarea textarea-primary shadow-xl h-80 w-full text-lg" 
                placeholder="Enter your text here..."
                bind:value={leftTextInput}
            ></textarea>

            <!-- Middle Button -->
            <div class="flex justify-center px-4">
                <button class="btn btn-primary btn-xl rounded-full font-bold text-2xl" onclick={textTransform}>
                    <b>→</b>
                </button>
            </div>

            <!-- Right Textbox -->
            <div class="relative">
                <textarea 
                    class="textarea textarea-accent shadow-xl h-80 w-full text-lg" 
                    placeholder="Transformed text will appear here..."
                    bind:value={rightTextInput}
                    readonly
                ></textarea>
                {#if rightTextInput.trim()}
                    <button
                        class="btn btn-sm absolute top-2 right-2 opacity-70 transition-all duration-200
                        {copyState === 'idle' 
                            ? 'btn-ghost hover:border-primary hover:bg-transparent' 
                            : copyState === 'success' 
                                ? 'bg-success text-success-content border-success' 
                                : 'bg-error text-error-content border-error'}"
                        onclick={copyToClipboard}
                        title="Copy to clipboard"
                        aria-label="Copy to clipboard."
                    >
                        {#if copyState === 'success'}
                            <!-- Checkmark icon for success -->
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                            </svg>
                        {:else if copyState === 'error'}
                            <!-- X icon for error -->
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                            </svg>
                        {:else}
                            <!-- Copy icon for idle -->
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path>
                            </svg>
                        {/if}
                    </button>
                {/if}
            </div>
        </div>
    </div>
</div>