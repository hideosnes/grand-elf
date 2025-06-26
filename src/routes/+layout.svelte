<script lang="ts">
    import '../app.css';

    let { children } = $props();
    let currentView = $state('transform');
	let currentYear = new Date().getFullYear();
</script>

<div class="flex flex-col">
    <!-- Top Menu -->
    <div class="navbar bg-base-100 flex-shrink-0">
        <div class="navbar-start"></div>     
        <div class="navbar-center">
            <div class="flex items-center gap-8">
                <div class="flex gap-6">
                    <button
                        class="text-lg transition-colors
                        {currentView === 'transform' 
                            ? 'text-primary font-bold' 
                            : 'text-base-content/60 hover:text-base-content'}"
                        onclick={() => currentView = 'transform'}
                    >Grand-Elf</button>
                    <button
                        class="text-lg transition-colors
                        {currentView === 'info' 
                            ? 'text-primary font-bold' 
                            : 'text-base-content/60 hover:text-base-content'}"
                        onclick={() => currentView = 'info'}
                    >Info</button>
                </div>
                
                <!-- GitHub link without logo -->
                <a
                    href="https://github.com/hideosnes/grand-elf"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="text-lg font-medium text-base-content/60 hover:text-primary transition-colors"
                >GitHub</a>
            </div>
        </div>
        
        <div class="navbar-end"></div>
    </div>

    <main data-theme="synthwave" class="flex-1">
        {#if currentView === 'transform'}
            {@render children()}
        {:else}
            <!-- Info View -->
            <!-- Changed: Removed h-full and overflow-hidden to allow natural height -->
            <div class="bg-base-100 p-8">
                <div class="max-w-3xl mx-auto">
                    <h1 class="text-3xl font-bold text-center m-8 text-primary">About Grand Elf</h1>
                    <div class="card bg-base-200 shadow-xl">
                        <div class="card-body">
                            <p class="text-lg">Info goes here...</p>
                        </div>
                    </div>
                </div>
            </div>
        {/if}
    </main>

	<footer class="footer footer-center p-4 bg-base-100 text-base-content/40 flex-shrink-0">
        <div class="flex items-center justify-center gap-4 text-xs">
            <span>© {currentYear} 
                <a 
                    href="https://hideosnes.online" 
                    target="_blank" 
                    rel="noopener noreferrer"
                    class="link link-hover text-base-content/50 hover:text-base-content/70"
                >Hidéo Snes</a>
            </span>
            <span class="text-base-content/60">|</span>
            <span class="text-base-content/60">You are not being tracked.</span>
        </div>
    </footer>
</div>