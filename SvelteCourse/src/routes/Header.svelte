<!--Script:-->
<script lang="ts">
    let {
        name,
        fake_name = null, // i can set default value here, fake_name = 'Pershing'
    }: {
        name: string;
        fake_name ?: string | null;
    } = $props();
</script>
<!--HTML-->
<!--Runes: with $ - are important-->

<h1>Hello {name}</h1>
<h2>{name.replaceAll('a', 'X')}</h2>
{fake_name}
<!--CSS-->
<style>
    h1 {
        color: red;
    }
</style>