<script>
    import {onMount} from "svelte";
    import { fade } from 'svelte/transition';
    let observer;
    let isVisible = false;
    let element;
    let fadeHappened = false;

    onMount(() => {
        observer = new IntersectionObserver(([entry]) => {
            isVisible = entry.isIntersecting;
            if(!fadeHappened && isVisible)
                fadeHappened = true;
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
    {#if fadeHappened}
    <div class="container" in:fade={{duration: 750, delay: 500}}>
        <div class="section__titles">
            <h3>FRAMEWORKS</h3>
            <h3>LANGUAGES</h3>
        </div>
        <div class="section__text">
            <h4>Angular / SvelteKit /<br>.NET Core</h4>
            <h4>TypeScript / JavaScript /<br>C# / Python</h4>
        </div>

        <div class="section__text">
            <h4>Data Structures /<br>Data Sc. / UI/UX</h4>
            <h4>CI/CD / REST APIs /<br>SQL Server / Oracle </h4>
        </div>
        <div class="section__titles">
            <h3>INTERESTS</h3>
            <h3>OTHER</h3>
        </div>
    </div>
        {/if}
</section>


<style lang="scss">
    section{
      padding-bottom: 6vw;
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

    .section__titles{
      display: flex;
      justify-content: space-between;
      &:first-of-type{
        margin-top: 5vw;
      }
      h3{
        font-family: var(--ff-text);
        font-weight: normal;
        font-size: 1vw;
      }
    }


    .section__text{
      display: flex;
      justify-content: space-between;
      &:nth-of-type(3){
        margin-top: 15vw;
      }
      h4{
        font-family: var(--ff-title);
        font-size: 4vw;
        margin: 0;
        &:last-of-type{
          text-align: right;
        }
      }
    }


    @media screen and (max-width: 700px){
      h2{
        font-size: 1.5vw;
      }
      .section__titles{
        h3{
          font-size: 1.5vw;
        }
      }
    }
</style>