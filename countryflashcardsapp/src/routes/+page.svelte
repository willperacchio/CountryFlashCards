<div class="font-mono">
    <div class="flex items-center justify-center">
        <div>
            <p>List of Countries</p>
        </div>
        <div>
            {#each categories as category}
                <p><input type="checkbox" class="rounded text-pink-500" id="${category}-check"/>{category}</p>
            {/each}
        </div>  
    </div>
    <div class="flex items-center justify-center">
        <div class = "wrapper w-3/4 h-3/4 ">
            <Grid
                {data}
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
            <!-- <a class="bg-sky-500 p-5 text-white rounded-full hover:bg-sky-700" href="/static/countryanki.csv" download>
                Generate CSV
            </a>               -->
            <button class="bg-sky-500 p-5 text-white rounded-full hover:bg-sky-700" on:click={exportToCsv}>
                Generate CSV
            </button> 
        </div>
    </div>
</div>

<script lang="ts">
import Grid from "gridjs-svelte";
import { html, h } from "gridjs"
import { RowSelection } from "gridjs/plugins/selection";
import "gridjs/dist/theme/mermaid.css";

let buttonHeaderGen = (text: String) => {
    return text; // html(`<input type="checkbox" class="rounded" value="${text}"/>${text}`)
};

function exportToCsv() {
    let csv = ""
    csv += "data:text/csv;charset=utf-8,";
    csv += "\nCountry Code, Country Name, Capital";
    csv += "\nUS, United States, Washington D.C.";
    // document.write(csv);

    var blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
    var url = URL.createObjectURL(blob);
    var link = document.createElement("a");
    link.setAttribute("href", url);
    link.setAttribute("download", "countryanki.csv");
    link.style.visibility = 'hidden';
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    return;
};

let categories = ["ISO Code", "Country Name"];

let columns = [
        {
            id: 'myCheckbox',
            name: 'Select',
            plugin: {
                component: RowSelection,
            }
        },
        {
            name: buttonHeaderGen("ISO Code"),
            id: "code"
        },
        {
            name: buttonHeaderGen("Country Name"),
            id: "name"
        },
        {
            name: buttonHeaderGen("Capital"),
            id: "capital"
        },
        {
            name: buttonHeaderGen("Country Outline"),
            id: "outline",
            formatter: (cell: String) => html(`<img class="h-36 object-center" src='${cell}'/>`)
        }
    ]

let className = {
    td: 'h-2'
}

let data = [
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