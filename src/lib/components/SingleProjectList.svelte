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

        const x = document.querySelectorAll('.follower');

        setTimeout(()=>{x[0].style.backgroundImage = `url("/images/01/1.png")`}, 100);
        setTimeout(()=>{x[0].style.backgroundImage = `url("/images/01/2.png")`}, 200);
        setTimeout(()=>{x[0].style.backgroundImage = `url("/images/01/3.png")`}, 300);
        setTimeout(()=>{x[1].style.backgroundImage = `url("/images/02/1.png")`}, 400);
        setTimeout(()=>{x[1].style.backgroundImage = `url("/images/02/2.png")`}, 500);
        setTimeout(()=>{x[1].style.backgroundImage = `url("/images/02/3.png")`}, 600);
        setTimeout(()=>{x[2].style.backgroundImage = `url("/images/03/1.png")`}, 700);
        setTimeout(()=>{x[2].style.backgroundImage = `url("/images/03/2.png")`}, 800);
        setTimeout(()=>{x[2].style.backgroundImage = `url("/images/03/3.png")`}, 900);
        setTimeout(()=>{x[3].style.backgroundImage = `url("/images/04/1.png")`}, 1000);
        setTimeout(()=>{x[3].style.backgroundImage = `url("/images/04/2.png")`}, 1100);
        setTimeout(()=>{x[3].style.backgroundImage = `url("/images/04/3.png")`}, 1200);

        document.addEventListener('scroll', ()=>{
            x.forEach((a) =>{
                a.style.display = 'none'
            })
        })

        const projects = document.querySelectorAll('.project');
        projects[3].addEventListener('click', (event) => {
            event.preventDefault();
            return false;
        })
        projects[4].addEventListener('click', (event) => {
            event.preventDefault();
            return false;
        })

        return () => {
            divElements.forEach(()=>{
                observer.disconnect();
            });
        };
    });

    let mouseX = 0;
    let mouseY = 0;
    let container;
    let follower;

    export let infos = {
        href: '',
        number: '',
        name: '',
        clientType: '',
        clientName: '',
        background: '',
    }

    function handleMouseMove(event) {
        const rect = container.getBoundingClientRect();
        mouseX = event.clientX - rect.left;
        mouseY = event.clientY - rect.top;
        follower.style.left = mouseX + 'px';
        follower.style.top = mouseY + 'px';
    }

    let index = 1;
    let intervals = [];
    let idInterval;
    function onHover(event){
        const element = event.currentTarget;
        const follower = element.querySelector('.follower');
        clearInterval(idInterval);
        idInterval = setInterval(()=>{
            if(index<3){
                index++;
            }

            else
                index = 1;
            follower.style.backgroundImage = `url("/images/${infos.number}/${index}.png")`;
        },500)
        intervals.push(idInterval);
    }

    function displayImages(event){
        const element = event.currentTarget;
        const follower = element.querySelector('.follower');
        follower.style.display = 'block';
    }

    function hideImages(event){
        clearInterval(idInterval);
        const element = event.currentTarget;
        const follower = element.querySelector('.follower');
        follower.style.display = 'none';
        intervals.forEach((interval)=>clearInterval(interval));
    }
</script>
<div class="container">
    <a href={infos.href} target={infos.target} class="project" on:mousemove={(event)=>{handleMouseMove(event); displayImages(event)}} on:mouseover={onHover} on:mouseleave={hideImages} bind:this={container}>
        <div class="follower" bind:this={follower}></div>
        <h3><span>{infos.number}</span>{infos.name}</h3>
        <div class="client__info">
            <p>{infos.clientType}</p>
            <h4>{infos.clientName}</h4>
        </div>
    </a>
</div>
<div class="border" style="width: {isVisible[2] ? '100%' : '0'}" bind:this={divElements[2]}></div>



<style lang="scss">
  :global(a){
    color: currentColor;
    text-decoration: none;
  }
  :global(a:visited){
    color: currentColor;
    text-decoration: none;
  }
  .follower{
    display: none;
    position: absolute;
    width: 30vw;
    height: 15vw;
    pointer-events: none;
    transform: translate(-50%, -50%);
    background-position: center;
    background-size: cover;
    z-index: 2;
  }

    .border{
      height: .2vw;
      transition: all 900ms;
      background-color: var(--color-black);
      width: 0;
    }
    .project{
      cursor: none;
      position: relative;
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
          font-weight: normal;
          letter-spacing: 1px;
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
              width: 95%;
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
      .follower{
        display: none;
        visibility: hidden;
      }
      .project{
        p{
          font-size: 1.5vw;
        }
        h4{
          font-size: 2vw;
        }
      }
    }
</style>