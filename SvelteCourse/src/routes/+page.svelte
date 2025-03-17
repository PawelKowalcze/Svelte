
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
        name: '',
        birthday: '',
        step: 0,
        error: ''
    });
</script>
<main>
    <p>Step: {formState.step + 1} </p>
    {#if formState.error}
        <p class="error">{formState.error}</p>

    {/if}

    {#if formState.step === 0}
        <div>
            <label for="name"> Your name </label>
            <input type="text" id="name" bind:value={formState.name}/>
        </div>
        <button onclick={() => {
            if (formState.name === '') {
                formState.error = 'Name is required';
            } else {
                formState.step += 1;
                formState.error = '';
            }
        }}> Next </button>

        {:else if formState.step === 1}
        <div>
            <label for="bday"> Your birthday </label>
            <input type="date" id="bday" bind:value={formState.birthday}/>
        </div>
        <button onclick={() => {
            if (formState.name === '') {
                formState.error = 'Write your birthday';
            } else {
                formState.step += 1;
                formState.error = '';
            }
        }}> Next </button>

    {/if}


</main>

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

