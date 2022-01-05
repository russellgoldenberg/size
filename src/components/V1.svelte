<script>
  import data from "$data/small.csv";
  import { scalePow, extent, format } from "d3";

  const phrases = ["does size matter", "does size really matter"];

  const markup = ({ lower, really }) => {
    const phrase = really ? phrases[1] : phrases[0];
    const start = lower.indexOf(phrase);
    const end = start + phrase.length;
    const before = lower.substring(0, start);
    const after = lower.substring(end, lower.length);
    return `${before}<mark>${phrase}</mark>${after}`;
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

  const extents = extent(papers.map((d) => d.citations));

  const fontScale = scalePow().exponent(0.25).domain(extents).range([12, 48]);
</script>

<section id="chart">
  <div>
    {#each papers as { lower, citations, markup }}
      <p class="paper" style="font-size: {Math.round(fontScale(citations))}px;">
        🍆 {@html markup}
      </p>
    {/each}
  </div>
</section>

<!-- <Footer /> -->
<style>
  #chart {
    margin: 2rem auto;
    padding: 2em;
  }

  div {
    overflow: hidden;
  }

  .paper {
    /* white-space: nowrap; */
    /* text-align: center; */
    line-height: 1.65;
    display: inline;
    padding: 0.125em;
    margin: 0;
    color: var(--color-gray-dark);
  }

  .paper:nth-of-type(even) {
    background: var(--color-off-white);
  }

  .paper:hover {
    background: var(--color-gray-light);
    color: var(--color-black);
  }
</style>
