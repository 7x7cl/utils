<script>
    import { graphQlQueryToJson } from "graphql-query-to-json";

    let graphQl = `{
  hero {
    name
  }
}`;

    function graphQlQueryToJsonErrorCatch(graphQl) {
        try {
            return JSON.stringify(graphQlQueryToJson(graphQl), null, 4);
        } catch (error) {
            return "No se pudo parsear";
        }
    }
    $: graphQlToJson = graphQlQueryToJsonErrorCatch(graphQl);

    function copy(graphQlToJson) {
        var textArea = document.getElementById("copy");
        textArea.value = graphQlToJson;
        textArea.select();
        document.execCommand("Copy");
    }
</script>

<textarea
    style="width:10px; position:absolute; z-index: -100 !important;"
    id="copy"
/>

<textarea bind:value={graphQl} />

<pre on:click={copy(graphQlToJson)}>{graphQlToJson}</pre>

<style>
    textarea {
        width: 100%;
        height: 200px;
    }
</style>
