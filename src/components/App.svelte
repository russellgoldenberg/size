<script>
  import V from "$components/V1.svelte";
  import Footer from "$components/Footer.svelte";
</script>

<section id="intro">
  <h1>academia's curious fixation with this platitudinous phallic phrase</h1>

  <details>
    <summary>why am i looking at this? 👀</summary>
    <p>
      i was doing "real" research on google scholar, and a paper grabbed my attention with a very
      dubious usage of "does size matter?" i thought that was strange, so I searched to see if how
      common it was. sure enough, i found over 1,000 results in the past 20 years, most not dealing
      with male anatomy.
    </p>
  </details>

  <p>
    <mark>"does size (really) matter?"</mark> is in the title of 1,004 papers on
    <a href="https://scholar.google.com/" target="_blank">google scholar</a>. only eight are about
    male anatonmy. bigger font means... more citations.
  </p>
</section>

<V />

<!-- <Footer /> -->
<style>
  #intro {
    max-width: 40rem;
    margin: 2rem auto;
  }
</style>
