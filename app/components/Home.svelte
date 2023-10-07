<script lang="ts">
    let message: string = "Blank Svelte Native App"
</script>

<page>
    <actionBar title="Home" />
    <gridLayout>
        <label class="info">
            <formattedString>
                <span class="fas" text="&#xf135;" />
                <span text=" {message}" />
            </formattedString>
            <formattedString>
                <p>Hello world</p>
            </formattedString>
        </label>
    </gridLayout>
</page>


<style>
    .info .fas {
        color: #3A53FF;
    }

    .info {
        font-size: 20;
        horizontal-align: center;
        vertical-align: center;
    }
</style>
