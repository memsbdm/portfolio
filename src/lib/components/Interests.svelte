<script>
    import {onMount} from "svelte";

    let observer;
    let isVisible = false;
    let element;

    onMount(() => {
        observer = new IntersectionObserver(([entry]) => {
            isVisible = entry.isIntersecting;
        });

        observer.observe(element);

        return () => {
            observer.disconnect();
        };
    });
</script>

<section>
    <div class="container">
        <h2>INTERESTS / SKILLS</h2>
    </div>
    <div class="border" style="width: {isVisible ? '100%' : '0'}" bind:this={element}></div>

</section>


<style lang="scss">
    section{
      height: 100vh;
    }
    h2{
      font-size: 1.25vw;
      letter-spacing: 1px;
      font-family: var(--ff-text);
    }
    .border{
      height: .2vw;
      transition: all 900ms;
      background-color: var(--color-black);
      width: 0;
    }


    @media screen and (max-width: 700px){
      h2{
        font-size: 1.5vw;
      }
    }
</style>