<script lang="ts">
    import { writable, type Writable } from 'svelte/store';
    import { Connectivity } from '@nativescript/core';
    import Home from './components/Home.svelte'
    import NotConnected from './components/NotConnected.svelte';
    
    /** Verify that user is connected to network or not */
    class ConnectionInternet {
        connected:  Writable<boolean> = writable(false)
        constructor() {
            this.connected.update(v => {
                v = this.isConnected();
                return v;
            });
            
            // Annotate and test whether user is still connected after connaction state change
            Connectivity.startMonitoring(cnType => {
                this.connected.update(v => {
                    v = this.isConnected()
                    return v;
                })
            });
        }
        
        protected isConnected(): boolean {
            const cn = Connectivity.getConnectionType()
            return cn == 1 || cn == 2 || cn == 3;
        }
    }

    const { connected } = new ConnectionInternet();
</script>

<frame>
    {#if $connected}
        <Home/>
    {:else}
        <NotConnected/>
    {/if}
</frame>
