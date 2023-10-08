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
        <flexboxLayout class="layout" flexDirection="column" justifyContent="center" alignItems="center">
            <stackLayout class="btn-img" data-polsat orientation="horizontal" padding="5" on:tap={selected.selectNew("polsat")} >]
                <image class="img" src="~/images/polsat-news.png"/>
                <label class="label" text="POLSAT NEWS"/>
            </stackLayout>
            <stackLayout class="btn-img" data-tvp orientation="horizontal" padding="5" on:tap={selected.selectNew("tvp")} >]
                <image class="img" src="~/images/tvp-info-logo.png"/>
                <label class="label" text="TVP INFO" color="black"/>
            </stackLayout>
            <stackLayout class="btn-img" data-tvn orientation="horizontal" padding="5" on:tap={selected.selectNew("tvn")} >]
                <image class="img" src="~/images/tvn-24.png"/>
                <label class="label" color="black">TVN 24</label>
            </stackLayout>
        </flexboxLayout>
    {:else}
        <webView src="{selected.getNewsUrl()}"/>
    {/if}
</page>

<style>
    .main {
        background-color: rgb(8, 112, 164);
    }

    .btn-img {
        width: 75%;
        height: 400px;
        background-color: white;
        margin-top: 45px;
        border-radius: 50px;
    }

    [data-polsat] {
        background-color: rgb(0, 0, 0);
    }

    [data-tvp] {
        background-color: whitesmoke;
    }

    [data-tvn] {
        background-color: white;
    }

    .img {
        width: 55%;
        height: 100%;
        object-fit: fill;
    }

    .label {
        width: 45%;
        height: 100%;
        text-align: center;
        color: white;
        font-size: 16px;
        font-weight: 600;
    }
</style>
