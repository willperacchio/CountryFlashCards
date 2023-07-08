<div class="font-mono">
    <div class="flex items-center justify-center">
        <p class="font-mono">List of Countries</p>
    </div>
    <div class="flex items-center justify-center">
        <div class = "wrapper w-3/4 h-3/4 ">
            <Grid data={countries} 
                {columns}
                sort
                search
                {className}
                fixedHeader
                resizable
                height="600px"
            />
        </div>
    </div>
    <div class="flex items-center justify-center">
        <div class = "wrapper h-1/4 pt-4">
            <button class="bg-sky-500 p-5 text-white rounded-full hover:bg-sky-700">
                Generate JSON
            </button>              
        </div>
    </div>
</div>

<script>
import Grid from "gridjs-svelte";
import { html, h } from "gridjs"
import "gridjs/dist/theme/mermaid.css";

let columns = [
    {
        name: "Checkbox",
        id: "code",
        formatter: (cell) => html(`<input type="checkbox" class="rounded" value='${cell}'/>`)
    },
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
        formatter: (cell) => html(`<img class="h-36 object-center" src='${cell}'/>`)
    }
]

let className = {
    td: 'h-2'
}

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
    },
    {
        "code": "AU",
        "name": "Australia",
        "capital": "Canberra",
        "outline": "../../outlines/AU.png"
    },
    {
        "code": "CA",
        "name": "Canada",
        "capital": "Ottawa",
        "outline": "../../outlines/CA.png"
    }
];

</script>

<style lang="postcss">
  :global(html) {
    background-color: theme(colors.gray.100);
    import: "https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css";
  }
</style>