<script>
  import V from "$components/V1.svelte";
  import Footer from "$components/Footer.svelte";
</script>

<section id="intro">
  <h1>academia's curious fixation with this platitudinous phallic phrase</h1>

  <details>
    <summary>why am i looking at this? 👀</summary>
    <p>
      i was doing "real" research on google scholar when a paper grabbed my attention with a very
      dubious usage of "does size matter?" i thought that was strange, so I searched to see if how
      common it was.
    </p>
    <p>
      there has been particular emphasis in western culture in the past century around this topic.
      according to <a
        href="https://psycnet.apa.org/doiLanding?doi=10.1037%2F1524-9220.7.3.129"
        target="_blank">one study</a
      > below, "popular media, especially TV and men's magazines, frequently emphasize the connection
      between penis size and masculinity. Pornographic movies, magazines, and Web sites featuring men
      with very large penises also reinforce the cultural message associating large penis size and masculinity."
    </p>

    <p>
      A <a
        href="https://books.google.com/ngrams/graph?content=does+size+matter&year_start=1500&year_end=2019&corpus=26&smoothing=3&direct_url=t1%3B%2Cdoes%20size%20matter%3B%2Cc0#t1%3B%2Cdoes%20size%20matter%3B%2Cc1"
        target="_blank">google ngram</a
      > query also paints the same picture, with the first occurence in the early 1900s. Its prevelance
      in the male pysche and public discouse is visible in the numerous attempts of playful paper titles.
      sure enough, i found over 1,000 results in the past 20 years or so, rarely about male anatomy.
    </p>
  </details>

  <p>
    <mark>"does size (really) matter?"</mark> is in the title of 1,004 papers on
    <a href="https://scholar.google.com/" target="_blank">google scholar</a>. only
    <mark class="hi">eight</mark> are about male anatonmy. bigger font means... more citations.
  </p>
</section>

<V />

<p>A project by <a href="https://pudding.cool/author/russell-goldenberg">Russell Goldenberg</a>.</p>
<Footer />

<style>
  #intro {
    max-width: 40rem;
    margin: 2rem auto;
  }

  .hi {
    padding: 0 0.25em;
  }

  details {
    cursor: pointer;
  }

  details p {
    padding: 1em;
    background: var(--color-purple-white);
  }
</style>
