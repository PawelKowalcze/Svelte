
<script lang="ts">
    import Header from "./Header.svelte";
    let name = $state('Pawel1');
    // let name = "Pawel";
    let status: 'OPEN' | 'CLOSED' = $state('OPEN');
    let full_name = $derived(name + ' ' + 'Kowalcze')
   //  1. Using function
   /* function toggle(){
        status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
    }*/

    // 2. Using onclick itself function
    // function onclick(){
    //     status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
    // }
</script>

<!--Here I can use my component-->
<Header {name} fake_name="Pershing"/>
<h2>{full_name}</h2>

<input type="text" bind:value={name}/>

<p>The store is now {status}</p>
<!--1. <button onclick={toggle}> Toggle Status </button>-->
<!--2. <button {onclick}> Toggle Status </button>-->
<!--3. Writing inline, unnamed function-->
<button onclick={() => {
    status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
}}> Toggle Status </button>

