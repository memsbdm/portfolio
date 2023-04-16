<div class="test"><div class="sun"><div class="line1"></div><div class="line2"></div><div class="line3"></div><div class="line4"></div></div></div>
<style lang="scss">

    .sun{
      position: absolute;
      width: 20px;
      z-index: 2;
      height: 20px;
      border-radius: 50%;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%) scale(1.5);
      transition: all 300ms;
      display: none;
      &::after{
        content: "";
        position: absolute;
        background-color: black;
        width: 100%;
        height: 100%;
        border-radius: 50%;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        box-shadow: 0 0 0 2px var(--color-white);
      }
    }
    .test{
      margin: 20rem auto;
      width: 2rem;
      height: 2rem;
      background-color: black;
      border-radius: 50%;
      position: relative;
      cursor: pointer;
      transition: all 300ms;
      &::before{
        content: "";
        position: absolute;
        width: 1.5rem;
        height: 1.5rem;
        right: -0.25rem;
        top: -0.25rem;
        background-color: var(--color-white);
        border-radius: 50%;
        transition: all 600ms;
        pointer-events: none;
      }
      &:hover{
        .sun{
          animation: passToSun 1000ms forwards;
        }
        rotate: 180deg;
        &::before{
          right: -1.5rem;
          top: -1.5rem;
          z-index: -1;
        }
      }
    }

    @keyframes passToSun {
      0%{
        transform: translate(-50%, -50%) scale(0);
      }
      50%{
        transform: translate(-50%, -50%) scale(1.7);
      }
      100%{
        transform: translate(-50%, -50%) scale(1.5);
      }
    }

    .line1{
      width: 2rem;
      height: 2px;
      background-color: black;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    .line2{
      width: 2rem;
      height: 2px;
      background-color: black;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) rotate(45deg);
    }
    .line3{
      width: 2px;
      height: 2rem;
      background-color: black;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) rotate(45deg);
    }
    .line4{
      width: 2px;
      height: 2rem;
      background-color: black;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) rotate(0deg);
    }

</style>

<script>
    import {onMount} from "svelte";

    onMount(()=>{
        const x = document.querySelector('.test');
        const y = document.querySelector('.sun');

        x.addEventListener('click', ()=>{
            y.style.display = 'block';
        })

        y.addEventListener('click', ()=>{
            y.style.display = 'none';
        })
    })
</script>