<script>
    import {onMount} from "svelte";

    onMount(()=>{
        window.scrollTo({
            top: 0,
            left: 0,
        });

        const logo = document.querySelector('header svg');
        const switchMode = document.querySelector('.switch__mode');
        const circle = document.querySelector('.circle');
        const lines = document.querySelector('.lines');
        const hideCircle = document.querySelector('.hide__circle');
        let moon = true;

        const handleClick = () => {
            if(moon){
                setTimeout(()=>{
                    lines.style.transform = 'scale(1)';
                    circle.style.transform = 'rotate(90deg) scale(0.6)';
                    hideCircle.style.top = '-1rem';
                    hideCircle.style.right = '-1rem';
                    hideCircle.style.transform = 'scale(0)';
                }, 300)

                document.documentElement.style.setProperty('--color-black', 'rgb(255, 248, 235)');
                document.documentElement.style.setProperty('--color-white', '#111010FF');
            }
            else{
                setTimeout(()=>{
                    lines.style.transform = 'scale(0)';
                    circle.style.transform = 'unset';
                    hideCircle.style.top = '-.1rem';
                    hideCircle.style.right = '-.1rem';
                    hideCircle.style.transform = 'scale(1)';
                }, 300)

                document.documentElement.style.setProperty('--color-black', '#111010FF');
                document.documentElement.style.setProperty('--color-white', 'rgb(255, 248, 235)');
            }
            moon = !moon;
        }

        switchMode.addEventListener('click', handleClick)

        const handleMouseOver = () => {
            if(moon){
                circle.style.transform = 'rotate(90deg)';
                hideCircle.style.top = '-3rem';
                hideCircle.style.right = '-3rem';
            }
            else{
                circle.style.transform = 'rotate(90deg) scale(1)';
            }
        }

        circle.addEventListener('mouseover', handleMouseOver)

        const handleMouseLeave = () => {
            if(moon){
                circle.style.transform = 'rotate(0deg)';
                hideCircle.style.top = '-.1rem';
                hideCircle.style.right = '-.1rem';
            }
            else{
                circle.style.transform = 'rotate(90deg) scale(0.6)';
            }
        }

        circle.addEventListener('mouseleave', handleMouseLeave)

        const scrollToTop = () => {
            window.scrollTo({
                top: 0,
                left: 0,
                behavior: "smooth",
            });
        };

        logo.addEventListener('click', scrollToTop);

        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();

                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });

        return ()=>{
            logo.removeEventListener('click', scrollToTop);
            switchMode.removeEventListener('click', handleClick)
            circle.removeEventListener('mouseover', handleMouseOver)
            circle.removeEventListener('mouseleave', handleMouseLeave)
        }
    })


</script>
<div class="container">
    <header>
        <svg width="134" height="65" viewBox="0 0 134 65" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M23.3288 63.845H-0.527512C-0.256047 62.7905 -0.0605925 61.9642 0.189155 61.1488C6.26996 41.0797 12.3833 21.0105 18.4316 0.91956C18.9419 -0.765555 19.6043 -1.5157 21.5154 -1.49396C27.9763 -1.41786 34.4371 -1.49396 40.8871 -1.66791C42.5919 -1.71139 43.2434 -1.10258 43.6778 0.452076C45.5237 7.06207 47.4891 13.6395 49.4111 20.2168C49.6283 20.9561 49.8889 21.6845 50.3558 23.1305C50.8227 21.7063 51.0942 20.9344 51.3222 20.1407C53.2333 13.6395 55.177 7.13818 56.9904 0.60428C57.4573 -0.993861 58.0763 -1.71139 59.9114 -1.66791C66.6871 -1.5157 73.4629 -1.5157 80.2495 -1.55919C81.6937 -1.55919 82.3126 -1.11345 82.7252 0.310744C88.6975 20.9996 94.7457 41.6776 100.761 62.3447C100.87 62.7144 100.957 63.0949 101.109 63.6928C100.294 63.758 99.6321 63.8559 98.9588 63.8668C92.5848 63.9537 86.2 63.9537 79.826 64.1277C78.1103 64.1712 77.3285 63.7254 76.829 61.9968C72.073 45.6893 67.2192 29.4143 62.3871 13.1176C62.2025 12.5088 61.9745 11.9217 61.6162 10.878C61.247 11.9109 61.0081 12.5414 60.8018 13.172C58.7278 19.7928 56.5995 26.4028 54.645 33.0563C54.2649 34.3392 54.2432 35.9047 54.6015 37.1876C56.7189 44.7978 58.9992 52.3536 61.2144 59.9312C61.551 61.0727 61.8333 62.2143 62.2025 63.5623C61.5293 63.6493 61.0189 63.7689 60.5086 63.7689C53.8848 63.7906 47.272 63.7363 40.6482 63.8559C38.9869 63.8885 38.3354 63.3884 37.8684 61.7794C33.2644 45.7545 28.5735 29.7513 23.9043 13.7482C23.6654 12.9219 23.3722 12.0957 22.8836 10.6171C21.4503 15.3137 20.2015 19.3906 18.9745 23.4566C18.0081 26.6638 17.172 29.9144 16.0753 33.0781C15.3477 35.1654 15.4672 37.0571 16.097 39.1227C18.3556 46.5264 20.5056 53.9626 22.699 61.3771C22.9162 62.1273 23.1008 62.8883 23.3397 63.8015L23.3288 63.845Z" fill="var(--color-black)"/>
            <path d="M121.784 29.1541C124.759 26.9363 125.367 23.8379 125.139 20.4133C124.248 6.62796 108.612 -4.50467 94.952 -0.83003C95.1258 -0.134241 95.2235 0.398473 95.3755 0.920315C99.48 15.0209 103.552 29.1215 107.7 43.2004L108.026 44.2767L113.759 63.3131C113.759 63.3131 113.77 63.3131 113.781 63.3239C113.965 63.4109 115.496 64.0849 118.439 64.1284C119.688 64.161 121.208 64.0632 122.989 63.7697H122.913C123.391 63.7153 123.868 63.5305 124.335 63.4C129.83 61.9215 133.044 58.2577 133.804 52.637C135.02 43.5809 129.971 33.6442 121.784 29.1541Z" fill="var(--color-black)"/>
        </svg>

        <span class="release-date">04.2023</span>
        <div class="switch__mode">
            <div class="lines">
                <div class="line line1"></div>
                <div class="line line2"></div>
                <div class="line line3"></div>
                <div class="line line4"></div>
            </div>
            <div class="circle"><div class="hide__circle"></div></div>
        </div>
    </header>
</div>
<slot></slot>



<style lang="scss">
    :root{
        --color-black: #111010FF;
        --color-white: rgb(255, 248, 235);
        --color-red: #C92D1F;
        --ff-title: Freight, sans-serif;
        --ff-text: Alte Haas Grotesk, sans-serif;
    }



    :global(body){
        background-color: var(--color-white);
        margin: 0;
        padding: 0;
        color: var(--color-black);
    }

    :global(.container){
        padding: 0 20px;
    }

    header{
        position: fixed;
        z-index: 98;
        padding: 0 20px;
        top: 0;
        left: 0;
        right: 0;
        display: flex;
        align-items: center;
        justify-content: space-between;
      background-color: var(--color-white);
    }

    svg{
        width: 2.5rem;
        cursor: pointer;
    }

    svg path {
        fill: var(--color-black);
    }

    .release-date{
        font-family: var(--ff-text);
        font-weight: bold;
        font-size: .9rem;
    }

    .switch__mode{
      width: 1.5rem;
      height: 1.5rem;
      position: relative;
      .lines{
        height: 100%;
        width: 100%;
        position: absolute;
        transition: all 600ms;
        transform: scale(0);
        .line1{
          width: 1.5rem;
          height: 2px;
          background-color: var(--color-black);
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
        }
        .line2{
          width: 1.5rem;
          height: 2px;
          background-color: var(--color-black);
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%) rotate(45deg);
        }
        .line3{
          width: 2px;
          height: 1.5rem;
          background-color: var(--color-black);
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%) rotate(45deg);
        }
        .line4{
          width: 2px;
          height: 1.5rem;
          background-color: var(--color-black);
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%) rotate(0deg);
        }
      }
      .circle {
        height: 1.5rem;
        width: 1.5rem;
        background-color: var(--color-black);
        border-radius: 50%;
        transition: all 300ms;
        position: absolute;
        cursor: pointer;
        box-shadow: 0 0 0 2px var(--color-white);

      }
      .hide__circle{
        height: 1rem;
        width: 1rem;
        border-radius: 50%;
        top: -.1rem;
        right: -.1rem;
        background-color: var(--color-white);
        position: absolute;
        transition: all 600ms;
        pointer-events: none;
      }
    }

    @media screen and (max-width: 700px){
      .release-date{
        font-size: .75rem;
      }
    }
</style>