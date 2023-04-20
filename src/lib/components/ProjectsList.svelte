<script>
    import { onMount } from "svelte";
    import SingleProjectList from "$lib/components/SingleProjectList.svelte";
    let observer;
    let isVisible = [];
    let divElements = [];

    onMount(() => {
        divElements.forEach((element, index)=>{
            observer = new IntersectionObserver(([entry]) => {
                isVisible[index] = entry.isIntersecting;
            });
            observer.observe(element);
        })
        return () => {
            divElements.forEach(()=>{
                observer.disconnect();
            });
        };
    });

    let allInfos = [
        {
            href: 'https://avn-auto.fr',
            target: '_blank',
            number: '01',
            name: 'Detailing Center',
            clientType: 'AVN AUTO',
            clientName: 'SVELTEKIT',
            background: `url("/images/01/1.png")`,
        },
        {
            href: 'https://nazikebadem.com',
            target: '_blank',
            number: '02',
            name: 'Clinical Psychologist',
            clientType: 'NAZIKE BADEM',
            clientName: 'VANILLA JS',
            background: `url("/images/02/1.png")`,
        },
        {
            href: 'https://dev.azure.com/mehmetbadem/CesiEats',
            target: '_blank',
            number: '03',
            name: 'Authentication',
            clientType: 'Back-end Project',
            clientName: 'C# .NET Web API',
            background: `url("/images/03/1.png")`,
        },
        {
            href: '',
            target: '_self',
            number: '04',
            name: 'Web Scrapping',
            clientType: 'ML / DATA ANALYSIS',
            clientName: 'PYTHON (IN PROGRESS)',
            background: `url("/images/04/1.png")`,
        },
        {
            href: '',
            target: '_self',
            number: '05',
            name: 'This Website',
            clientType: 'PORTFOLIO',
            clientName: 'SVELTEKIT',
            background: `url("/images/05/1.png")`,
        },
    ]


</script>
<section>
    <div class="border" style="width: {isVisible[0] ? '100%' : '0'}" bind:this={divElements[0]}></div>
    <div class="container">
        <h2>SELECTED WORKS</h2>
    </div>
    <div class="border" style="width: {isVisible[1] ? '100%' : '0'}" bind:this={divElements[1]}></div>

    {#each allInfos as infos}
    <SingleProjectList {infos} />
    {/each}

</section>


<style lang="scss">
  :global(a){
    color: currentColor;
    text-decoration: none;
  }
  :global(a:visited){
    color: currentColor;
    text-decoration: none;
  }
    section{
      margin-top: 15vw;
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