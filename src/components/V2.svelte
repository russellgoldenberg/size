<script>
  import data from "$data/small.csv";
  import { scalePow, extent, format } from "d3";

  let chartWidth = 0;

  const phrases = ["does size matter", "does size really matter"];

  const getPos = (lower, phrase) => {
    const start = lower.indexOf(phrase);
    const end = start + phrase.length;
    return { start, end };
  };

  const getPhrase = (lower) => (lower.indexOf(phrases[1]) > -1 ? phrases[1] : phrases[0]);

  const markup = (lower) => {
    const phrase = getPhrase(lower);
    const { start, end } = getPos(lower, phrase);
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
      markup: markup(d.lower)
    }))
    .filter((d) => !d.lower.includes(phrases[1]));

  const extents = extent(papers.map((d) => d.citations));

  const fontScale = scalePow().exponent(0.25).domain(extents).range([12, 48]);

  const shift = (node, lower) => {
    const phrase = getPhrase(lower);
    const { start, end } = getPos(lower, phrase);
    const l = lower.length;
    const w = node.getBoundingClientRect().width;
    const center = (start + (end - start) / 2) / l;
    const offset = center * w;
    const transform = `translateX(-${offset}px)`;
    node.style.transform = transform;
    return {
      destroy() {
        // the node has been removed from the DOM
      }
    };
  };
</script>

<section id="chart">
  <div>
    {#each papers as { lower, citations, markup }}
      <p use:shift={lower} class="paper">
        {@html markup}
      </p>
    {/each}
  </div>
</section>

<style>
  #chart {
    margin: 2rem auto;
    padding: 2em;
  }

  div {
    overflow: hidden;
  }

  .paper {
    white-space: nowrap;
    line-height: 1;
    display: inline-block;
    color: var(--color-gray-dark);
    font-size: 20px;
    margin-left: 50%;
    margin-bottom: 0;
  }

  :global(mark) {
    background: transparent;
    font-weight: bold;
    color: var(--color-purple);
    padding: 0;
  }
</style>
