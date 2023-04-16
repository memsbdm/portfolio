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
        <div class="social__links">
            <div class="border" style="width: {isVisible[1] ? '100%' : '0'}" bind:this={divElements[1]}></div>
            <div class="top">
                <h3>SOCIAL LINKS</h3>
            </div>
            <div class="border" style="width: {isVisible[2] ? '100%' : '0'}" bind:this={divElements[2]}></div>

            <div class="bot">
                <a href="">INSTAGRAM</a>
                <a href="">LINKEDIN</a>
                <a href="">GITHUB</a>
                <a href="">TWITTER</a>
            </div>
            <div class="border" style="width: {isVisible[3] ? '100%' : '0'}" bind:this={divElements[3]}></div>
        </div>
        <div class="get__in__touch">
            <div class="border" style="width: {isVisible[4] ? '100%' : '0'}" bind:this={divElements[4]}></div>
            <div class="top">
                <h3>GET IN TOUCH</h3>
            </div>
            <div class="border" style="width: {isVisible[5] ? '100%' : '0'}" bind:this={divElements[5]}></div>

            <div class="bot">
                <p>NEW BUSINESS:</p>
                <a href="">mehmetbdm@outlook.fr</a>
                <p>PHONE:</p>
                <a href="">(+33)6 04 09 04 38</a>
            </div>
            <div class="border" style="width: {isVisible[6] ? '100%' : '0'}" bind:this={divElements[6]}></div>
        </div>
        <div class="collaborate">
            <p>Want to collaborate?</p>
        </div>
    </div>
</section>


<style lang="scss">
    section{
      font-family: var(--ff-text);
      letter-spacing: 3px;
      padding-bottom: 5vw;
    }
    h3{
        margin: 5vw 0;
        font-size: 1.25vw;
    }

    p{
      font-weight: bold;
      margin: 2vw 0 0 0;
      font-size: 1.25vw;
    }

    .social__links a{
      margin: .5vw 0 .5vw 0;
      &:first-of-type{
        margin-top: 2vw;
      }
    }
    a{
      font-size: 1.15vw;
    }

    .border{
      height: .2vw;
      transition: all 900ms;
      background-color: var(--color-black);
      width: 0;
    }
    .container{
      margin-top: 5vw;
      display: flex;
      justify-content: space-between;
      gap: 10vw;
    }
    .social__links, .get__in__touch{
      display: flex;
      flex-direction: column;
      width: 45%;
    }

    .social__links .top, .get__in__touch .top{
      height: 20%;
      display: flex;
      align-items: center;
    }

    .social__links .bot, .get__in__touch .bot{
      height: 80%;

    }

    .social__links .bot{
      display: flex;
      flex-direction: column;
    }
    .collaborate{
      width: 10%;
      display: flex;
      justify-content: center;
      align-items: center;
      p{
        margin: 0;
        font-size: 4.2vw;
        font-family: var(--ff-title);
        transform:  rotate(90deg);
      }
    }

    @media screen and (max-width: 700px){
      h3{
        font-size: 2vw;
      }
      p{
        font-size: 2vw;
      }
      a{
        font-size: 1.9vw;
      }
      .social__links a{
        margin: 1vw 0;
      }
    }
</style>