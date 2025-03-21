
<script lang="ts">
    import Header from "./Header.svelte";
   //  let name = $state('Pawel1');
   //  // let name = "Pawel";
   //  let status: 'OPEN' | 'CLOSED' = $state('OPEN');
   //  let full_name = $derived(name + ' ' + 'Kowalcze')
   // //  1. Using function
   // /* function toggle(){
   //      status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
   //  }*/
   //
   //  // 2. Using onclick itself function
   //  // function onclick(){
   //  //     status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
   //  // }

    let formState = $state({
        answers: {},
        step: 0,
        error: ''
    });

    const Questions = [
        {
            question: "What's your name?",
            id: 'name',
            type: 'text'
        },
        {
            question: "What's your birthday?",
            id: 'birthday',
            type: 'date'
        },
        {
            question: "What's your favorite color?",
            id: 'color',
            type: 'color'
        }

    ];

    function nextStep(id: string){
        if(formState.answers[id]){
            formState.step += 1;
            formState.error = '';
        } else {
            formState.error = 'Please answer the question';
        }
    }

    //Will run onMount
    $effect(() => {
        console.log('Mounted');
        return () => {
            // when unmounted or destroyed
            // before effect Re-runs
            console.log('Unmounted');
        };
    });

    $effect (() => {
        // This will rerun whien formState.step changes
        console.log('Step changed', formState.step);
        return () => {
            console.log('before formState.step Re-runs', formState.step);
        };
    });
    // Always runs when formState.step changes, you can check if variables are changing
    $inspect(formState.step,);
</script>

<Header name={formState.answers.name} fake_name="Pershing"/>
<!--    <p>Hello</p>-->
<!--&lt;!&ndash;Named child&ndash;&gt;-->
<!--&lt;!&ndash;    {#snippet secondChild(name)}&ndash;&gt;-->
<!--&lt;!&ndash;        <p>SecondChild {name}</p>&ndash;&gt;-->
<!--&lt;!&ndash;    {/snippet}&ndash;&gt;-->
<!--</Header>-->

<main>
    {#if formState.step === Questions.length}
        <p>Thank you for filling out the form</p>
    {:else}
        <p>Step: {formState.step + 1} </p>
    {/if}

    {#each Questions as question, index (question.id)}
        {#if formState.step === index}
            {@render formStep(question)}
            {/if}
    {/each}


<!--Instead of this i am doing it by snippet-->
    <!--{#if formState.step === 0}-->
    <!--    <div>-->
    <!--        <label for="name"> Your name </label>-->
    <!--        <input type="text" id="name" bind:value={formState.name}/>-->
    <!--    </div>-->
    <!--    <button onclick={() => {-->
    <!--        if (formState.name === '') {-->
    <!--            formState.error = 'Name is required';-->
    <!--        } else {-->
    <!--            formState.step += 1;-->
    <!--            formState.error = '';-->
    <!--        }-->
    <!--    }}> Next </button>-->

    <!--    {:else if formState.step === 1}-->
    <!--    <div>-->
    <!--        <label for="bday"> Your birthday </label>-->
    <!--        <input type="date" id="bday" bind:value={formState.birthday}/>-->
    <!--    </div>-->
    <!--    <button onclick={() => {-->
    <!--        if (formState.name === '') {-->
    <!--            formState.error = 'Write your birthday';-->
    <!--        } else {-->
    <!--            formState.step += 1;-->
    <!--            formState.error = '';-->
    <!--        }-->
    <!--    }}> Next </button>-->

    <!--{/if}-->

    {#if formState.error}
        <p class="error">{formState.error}</p>

    {/if}

</main>
{JSON.stringify(formState)}
<!--Its just a function, snippet is for rendering children-->
{#snippet formStep({question, type, id} : {question: string, type: string, id: string})}
    <article>
        <div>
            <label for ={id}>{question}</label>
            <input {type} {id} bind:value={formState.answers[id]}/>
        </div>
        <button onclick={() => nextStep(id)}> Next </button>
    </article>
{/snippet}


<!--CSS in svelte only affects items in current component-->
<style>
    /*:global(div){*/
    /*    background: blue;*/
    /*}*/
    .error {
        color: red;
    }
</style>




<!--&lt;!&ndash;Here I can use my component&ndash;&gt;-->
<!--<Header {name} fake_name="Pershing"/>-->
<!--<h2>{full_name}</h2>-->

<!--<input type="text" bind:value={name}/>-->

<!--<p>The store is now {status}</p>-->
<!--&lt;!&ndash;1. <button onclick={toggle}> Toggle Status </button>&ndash;&gt;-->
<!--&lt;!&ndash;2. <button {onclick}> Toggle Status </button>&ndash;&gt;-->
<!--&lt;!&ndash;3. Writing inline, unnamed function&ndash;&gt;-->
<!--<button onclick={() => {-->
<!--    status = status === 'OPEN' ? 'CLOSED' : 'OPEN';-->
<!--}}> Toggle Status </button>-->

