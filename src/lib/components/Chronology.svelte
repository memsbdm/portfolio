<div class="container">
    <section>
        <div class="controls">
            <div class="before" on:click={before}>
                <div class="line__before"></div>
                <span class="material-symbols-rounded">arrow_back_ios</span>
                <span class="before__text">BEFORE</span>
            </div>
            <div class="after" on:click={after}>
                <div class="line__after"></div>
                <span class="after__text">AFTER</span>
                <span class="material-symbols-rounded">arrow_forward_ios</span>
            </div>
        </div>
        <h4>{value}</h4>
        <div class="school__and__work">
            <div class="work">
                <h5>PROFESIONNAL EXPERIENCE</h5>
                {#key jobCompany}
                <h3 class="jobCompany" in:fade={{duration: 750}}>{jobCompany}</h3>
                {/key}
                {#key jobTitle}
                <h2 class="jobTitle" in:fade={{duration: 750}}>{jobTitle}</h2>
                {/key}
            </div>
            <div class="school">
                <h5>EDUCATION</h5>
                {#key schoolName}
                <h3 class="schoolName" in:fade={{duration: 750}}>{schoolName}</h3>
                {/key}
                {#key schoolClass}
                <h2 class="schoolClass" in:fade={{duration: 750}}>{schoolClass}</h2>
                {/key}
            </div>
        </div>
    </section>
</div>
<script>
    import { fade } from 'svelte/transition';
    $: value = 2023;
    $: changeInfos(value);
    $: jobCompany = "GROUPE BPCE";
    $: jobTitle = ".NET / ANGULAR DEVELOPER";
    $: schoolName = "CESI ÉCOLE D'INGÉNIEURS";
    $: schoolClass = "COMPUTER SC. ENGINEERING";

    const jobCompanies = ['N/A', 'COLIN INGRÉDIENTS GROUP', 'DIGITAL SERVICES PLATFORMS', 'WEINMANN TECHNOLOGIES', 'GROUPE BPCE'];
    const jobTitles = ['NEW BORN', 'FACTORY PRODUCTION WORKER', 'FRONT-END FREELANCER', 'COMPUTER SC. ENGINEER', '.NET / ANGULAR DEVELOPER'];
    const schoolNames = ['N/A', 'UNIVERSITY OF STRASBOURG', "CESI ÉCOLE D'INGÉNIEURS"];
    const schoolClasses = ['N/A', 'MATHEMATICS & COMPUTER SC.', 'COMPUTER SC. ENGINEERING', 'GRADUATED IN SEPT. 2024'];
    function changeInfos(value){
        switch (value){
            case 2000:
                jobCompany = jobCompanies[0];
                jobTitle = jobTitles[0];
                schoolName = schoolNames[0];
                schoolClass = schoolClasses[0];

                break;
            case 2020:
                jobCompany = jobCompanies[1];
                jobTitle = jobTitles[1];
                schoolName = schoolNames[1];
                schoolClass = schoolClasses[1];
                break;
            case 2021:
                jobCompany = jobCompanies[2];
                jobTitle = jobTitles[2];
                schoolName = schoolNames[1];
                schoolClass = schoolClasses[1];
                break;
            case 2022:
                jobCompany = jobCompanies[3];
                jobTitle = jobTitles[3];
                schoolName = schoolNames[2];
                schoolClass = schoolClasses[2];
                break;
            case 2023:
                jobCompany = jobCompanies[4];
                jobTitle = jobTitles[4];
                schoolName = schoolNames[2];
                schoolClass = schoolClasses[2];
                break;
            case 2024:
                jobCompany = jobCompanies[4];
                jobTitle = jobTitles[4];
                schoolName = schoolNames[2];
                schoolClass = schoolClasses[3];
                break;
            default:
                jobCompany = 'REMEMBERING...';
                jobTitle = 'REMEMBERING...';
                schoolName = 'REMEMBERING...';
                schoolClass = 'REMEMBERING...';
                break;
        }
    }

    function before(){
        const lineBefore = document.querySelector('.line__before');
        const lineAfter = document.querySelector('.line__after');
        if(value > 2024 || (value>2000 && value < 2020) || value < 2000)
            return;
        if(value === 2024)
            lineAfter.style.width = '2.75rem';
        if(value === 2020){
            for(let i=0; i<20; i++){
                setTimeout(()=>{value -= 1;},i*35)
            }
            lineBefore.style.width = 'calc(100% - 2px)';
        }
        if (value > 2020){
            value -= 1;
        }
    }

    function after(){
        const lineBefore = document.querySelector('.line__before');
        const lineAfter = document.querySelector('.line__after');
        if(value < 2000 || (value>2000 && value < 2020) || value > 2023)
            return;
        if(value === 2000){
            for(let i=0; i<19; i++){
                setTimeout(()=>{value += 1;},i*35)
            }
            lineBefore.style.width = '2.75rem';
        }
        if (value < 2024){
            value += 1;
            if(value === 2024)
                lineAfter.style.width = 'calc(100% - 2px)';
        }
    }
</script>

<style lang="scss">
    section{
      padding-top: 3rem;
    }
    .controls{
      display: flex;
      justify-content: space-between;
      font-family: var(--ff-text);
      font-weight: bold;
      color: var(--color-red);
      -webkit-touch-callout: none;
      -webkit-user-select: none;
      -khtml-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
      .before{
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 3rem;
        position: relative;
        .line__before{
          position: absolute;
          top: 50%;
          left: 2px;
          transform: translateY(-50%);
          height: 3px;
          width: 2.75rem;
          background-color: var(--color-red);
          transition: all 300ms;
        }
      }
      .after{
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 3rem;
        position: relative;
        .line__after{
          position: absolute;
          top: 50%;
          right: 2px;
          transform: translateY(-50%);
          height: 3px;
          width: 2.75rem;
          background-color: var(--color-red);
          transition: all 300ms;
        }
      }
    }

    h4{
      margin: 5vw 0;
      font-size: min(30vw, 320px);
      text-align: center;
      font-family: var(--ff-title);
      font-weight: normal;
    }

    .material-symbols-rounded {
        width: 1rem;
       font-variation-settings:
               'FILL' 0,
               'wght' 700,
               'GRAD' 0,
               'opsz' 48
     }

    .school__and__work{
      display: flex;
      justify-content: space-between;
      font-family: var(--ff-text);
    }
    h5{
      font-weight: normal;
      font-size: 1.25vw;
    }
    h3{
        margin-bottom: 0;
        font-size: 1.75vw;
    }
    h2{
        margin-top: 0;
        font-size: 2.25vw;
    }
    .work{

    }
    .school{
        text-align: right;
    }

    @media screen and (max-width: 700px){
      .controls{
        .before__text, .after__text{
            font-size: .7rem!important;
        }
        .before{
          .line__before{
            height: 2px;
          }
          span{
            font-size: 1.2rem;
          }
        }
        .after{
          .line__after{
            right: 3px;
            height: 2px;
          }
          span{
            font-size: 1.2rem;
          }
        }
      }
      h5{
        font-size: 2vw;
      }
      h3{
        font-size: 2.25vw;
      }
      h2{
        font-size: 2.75vw;
      }
    }
</style>