<div ref:content>
  {@html rendered}
</div>

<script>
import katex from 'katex';
import he from 'he';

export default {
  computed: {
    rendered: ({ html }) => html
        .replace(/\$\$[^$]+\$\$/g, equation => {
          const ren = katex.renderToString(he.decode(equation.slice(2, -2)))
          console.log(ren);
          return ren;
        })
  }
};
</script>
