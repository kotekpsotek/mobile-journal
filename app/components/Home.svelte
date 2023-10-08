<script lang="ts">
    let message = "Hello world"

    type ToSelect = "tvn" | "tvp" | "polsat";
    const selected: { select?: ToSelect, selectNew: (to: ToSelect) => any, getNewsUrl(): string, getNewsTitle(): string, getNewsTitle(): string } = {
        selectNew(toSelect) {
            return (ev: any) => {
                selected.select = toSelect
            }
        },
        getNewsUrl() {
            switch (this.select) {
                case "polsat":
                    return "https://www.polsatnews.pl/";
                case "tvp":
                    return "https://www.tvp.info/";
                case "tvn":
                    return "https://tvn24.pl/";
                default: 
                    return "";
            }
        },
        getNewsTitle() {
            switch (this.select) {
                case "polsat":
                    return "Polsat News"
                case "tvn":
                    return "TVN 24";
                case "tvp":
                    return "TVP INFO";
                default:
                    return "Pick news source"
            }
        }
    }
</script>

<page class="main">
    <actionBar title="{selected ? selected.getNewsTitle() : ""}"/>
    {#if !selected.select}
        <flexboxLayout flexDirection="row" justifyContent="center" alignItems="center">
            <button id="polsat" on:tap={selected.selectNew("polsat")}>POLSAT NEWS</button>
            <button id="tvp" on:tap={selected.selectNew("tvp")}>TVP INFO</button>
            <button id="tvn" on:tap={selected.selectNew("tvn")}>TVN 24</button>
        </flexboxLayout>
    {:else}
        <webView src="{selected.getNewsUrl()}"/>
    {/if}
</page>

<style>
    .main {
        background-color: black;
    }
</style>
