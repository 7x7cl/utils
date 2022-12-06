<script>
    import { jsonToGraphQLQuery } from "json-to-graphql-query";

    let graphQl = `{
    "query": {
        "Posts": {
            "id": true,
            "title": true,
            "post_date": true
        }
    }
}`;

    function jsonToGraphQLQueryErrorCatch(graphQl) {
        try {
            return jsonToGraphQLQuery(JSON.parse(graphQl));
        } catch (error) {
            return "No se pudo parsear";
        }
    }
    $: JsontoGraphQL = jsonToGraphQLQueryErrorCatch(graphQl);

    function copy(JsontoGraphQL) {
        var textArea = document.getElementById("copy");
        textArea.value = JsontoGraphQL;
        textArea.select();
        document.execCommand("Copy");
    }
</script>

<textarea
    style="width:10px; position:absolute; z-index: -100 !important;"
    id="copy"
/>

<textarea bind:value={graphQl} />

<pre on:click={copy(JsontoGraphQL)}>{JsontoGraphQL}</pre>

<style>
    textarea {
        width: 100%;
        height: 200px;
    }
</style>
