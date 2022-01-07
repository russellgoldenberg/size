<script>
  import data from "$data/small.csv";
  import { scalePow, extent, format, descending } from "d3";
  import viewport from "$stores/viewport.js";

  const phrases = ["does size matter", "does size really matter"];

  const markup = ({ lower, really, href }) => {
    const phrase = really ? phrases[1] : phrases[0];
    const start = lower.indexOf(phrase);
    const end = start + phrase.length;
    const before = lower.substring(0, start);
    const after = lower.substring(end, lower.length);
    return `${before}<a href="${href}" target="_blank">${phrase}</a>${after}`;
  };

  const papers = data
    .map((d) => ({
      ...d,
      lower: d.title.toLowerCase().trim(),
      citations: +d.citations
    }))
    .map((d) => ({
      ...d,
      really: d.lower.indexOf("does size really matter") > -1
    }))
    .map((d) => ({
      ...d,
      markup: markup(d)
    }));

  papers.sort((a, b) => descending(a.citations, b.citations));
  const extents = extent(papers.map((d) => d.citations));

  $: min = $viewport.width < 1200 ? ($viewport.width < 600 ? 12 : 14) : 16;
  $: max = $viewport.width < 1200 ? ($viewport.width < 600 ? 24 : 32) : 48;
  $: fontScale = scalePow().exponent(0.25).domain(extents).range([min, max]);
</script>

<section id="chart">
  <div>
    {#each papers as { lower, citations, markup, tag }}
      <p
        class="paper"
        class:hi={tag === "true"}
        style="font-size: {Math.round(fontScale(citations))}px;"
      >
        <span>🍆</span>
        {@html markup}
      </p>
    {/each}
  </div>
</section>

<!-- <Footer /> -->
<style>
  #chart {
    margin: 2rem auto;
  }

  div {
    overflow: hidden;
  }

  .paper {
    line-height: 1.5;
    display: inline;
    padding: 0.25em;
    margin: 0;
    color: var(--color-off-black);
  }

  .paper:nth-of-type(even) {
    background: var(--color-purple-white);
    color: var(--color-purple-dark);
  }

  .paper:hover {
    background: var(--color-purple-light);
    color: var(--color-black);
  }

  .hi {
    background: var(--color-green) !important;
  }

  :global(.paper a) {
    text-decoration: none;
    font-weight: bold;
  }

  :global(.paper a:hover) {
    border-bottom: 3px solid currentColor;
  }
</style>
