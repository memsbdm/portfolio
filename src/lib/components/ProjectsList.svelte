<script>
    import { onMount } from "svelte";
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
</script>
<section>
    <div class="border" style="width: {isVisible[0] ? '100%' : '0'}" bind:this={divElements[0]}></div>
    <div class="container">
        <h2>SELECTED WORKS</h2>
    </div>
    <div class="border" style="width: {isVisible[1] ? '100%' : '0'}" bind:this={divElements[1]}></div>
    <div class="container">
        <a href="" class="project">
            <h3><span>01</span>Detailing Center</h3>
            <div class="client__info">
                <p>CLIENT</p>
                <h4>AVN AUTO</h4>
            </div>
        </a>
    </div>
    <div class="border" style="width: {isVisible[2] ? '100%' : '0'}" bind:this={divElements[2]}></div>


    <div class="container">
        <a href="" class="project">
            <h3><span>02</span>Clinical Psychologist</h3>
            <div class="client__info">
                <p>CLIENT</p>
                <h4>NAZIKE BADEM</h4>
            </div>
        </a>
    </div>
    <div class="border" style="width: {isVisible[3] ? '100%' : '0'}" bind:this={divElements[3]}></div>


    <div class="container">
        <a href="" class="project">
            <h3><span>03</span>Web Scrapping</h3>
            <div class="client__info">
                <p>SIDE PROJECT</p>
                <h4>DATA ANALYSIS</h4>
            </div>
        </a>
    </div>
    <div class="border" style="width: {isVisible[4] ? '100%' : '0'}" bind:this={divElements[4]}></div>


    <div class="container">
        <a href="" class="project">
            <h3><span>04</span>This Website</h3>
            <div class="client__info">
                <p>SIDE PROJECT</p>
                <h4>PORTFOLIO</h4>
            </div>
        </a>
    </div>
    <div class="border" style="width: {isVisible[5] ? '100%' : '0'}" bind:this={divElements[5]}></div>



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
      padding-top: 3rem;
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
    .project{
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      padding: 3vw 0;
      transition: all 200ms;
      &:hover{
        color: var(--color-red);
        h3 span::before{
          background-color: var(--color-red);
        }
      }
        h3{
          margin: 0 0 0 3vw;
          font-family: var(--ff-title);
          font-size: 7vw;
          position: relative;
          span{
            position: absolute;
            top: 1vw;
            left: -3vw;
            font-family: var(--ff-text);
            font-weight: lighter;
            font-size: 1.5vw;
            &::before{
              content: "";
              position: absolute;
              height: .15vw;
              width: 100%;
              bottom: 0;
              left: 0;
              background-color: var(--color-black);
            }
          }
        }
      p{
        margin: 0;
        font-family: var(--ff-text);
        text-align: right;
        font-size: 1vw;
      }
      h4{
        margin: .2vw 0 0 0;
        font-family: var(--ff-text);
        text-align: right;
        font-size: 1.5vw;
      }
    }

    @media screen and (max-width: 700px){
      .project{
        p{
          font-size: 1.5vw;
        }
        h4{
          font-size: 2vw;
        }
      }
      h2{
        font-size: 1.5vw;
      }
    }
</style>