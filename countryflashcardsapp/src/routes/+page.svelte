<h1 class="text-3xl font-bold underline">
  Hello World!
</h1>

<h2>List of Countries</h2>
<div class="wrapper w-3/4 flex justify-center">
    <Grid data={countries} 
        {columns}
        sort
        search
        fixedHeader
    />
</div>

<script>
import Grid from "gridjs-svelte";
import { html } from "gridjs"
import "gridjs/dist/theme/mermaid.css";

let columns = [
    {
        name: "ISO Code",
        id: "code"
    },
    {
        name: "Country Name",
        id: "name"
    },
    {
        name: "Capital",
        id: "capital"
    },
    {
        name: "Country Outline",
        id: "outline",
        formatter: (cell) => html(`<img src='${cell}'/>`)
    }
]

let countries = [
    {
        "code": "US",
        "name": "United States",
        "capital": "Washington, D.C.",
        "outline": "../../outlines/US.png"
    },
    {
        "code": "UK",
        "name": "United Kingdom",
        "capital": "London",
        "outline": "../../outlines/GB.png"
    }
];

</script>

<style lang="postcss">
  :global(html) {
    background-color: theme(colors.gray.100);
    import: "https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css";
  }
</style>