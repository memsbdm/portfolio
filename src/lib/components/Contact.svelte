<script>
    import { onMount } from "svelte";
    let phoneNumber = '(+33)6 04 09 04 38';
    let email = 'mehmetbdm@outlook.fr';
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
    function copyEmail() {
        let timeoutId;
        navigator.clipboard.writeText(email).then(function() {
            document.querySelector('.copied p').style.opacity = '1';
            timeoutId = setTimeout(()=>{
                document.querySelector('.copied p').style.opacity = '0';
            },1000)
        }, function() {
            console.error("Email not copied.")
        });
        return clearTimeout(timeoutId);
    }

    function copyPhoneNumber() {
        let timeoutId;
        navigator.clipboard.writeText(phoneNumber).then(function() {
            document.querySelector('.copied p').style.opacity = '1';
            timeoutId = setTimeout(()=>{
                document.querySelector('.copied p').style.opacity = '0';
            },1000)
        }, function() {
            console.error("Phone number not copied.")
        });
        return clearTimeout(timeoutId);
    }

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
                <a href="https://fr.linkedin.com/in/mehmet-badem-b89b20189" target="_blank">LINKEDIN</a>
                <a href="https://github.com/memsbdm" target="_blank">GITHUB</a>
                <a href="https://www.instagram.com/memsbdm/" target="_blank">INSTAGRAM</a>
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
                <span on:click={copyEmail}>{email}</span>
                <p>PHONE:</p>
                <span on:click={copyPhoneNumber}>{phoneNumber}</span>
                <div class="copied">
                    <p>Copied to the clipboard!</p>
                </div>
            </div>
            <div class="border" style="width: {isVisible[6] ? '100%' : '0'}" bind:this={divElements[6]}></div>
        </div>
        <div class="collaborate">
            <p>Want to collaborate?</p>
        </div>
    </div>
</section>


<style lang="scss">
  .copied{
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    color: var(--color-red);
    margin-top: 1vw;
    font-size: 1.5vw;
    p{
      opacity: 0;
      transition: all 300ms;
      font-weight: normal;
    }
  }
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
    a, span{
      font-size: 1.15vw;
    }

    .get__in__touch span{
      cursor: pointer;
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
      a, span{
        font-size: 1.9vw;
      }
      .social__links a{
        margin: 1vw 0;
      }
    }
</style>