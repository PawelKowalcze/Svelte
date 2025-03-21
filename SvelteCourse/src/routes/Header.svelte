<!--Script:-->
<script lang="ts">
    import type {Snippet} from "svelte";

    let {
        name,
        fake_name = null, // i can set default value here, fake_name = 'Pershing'
        children,
        secondChild
    }: {
        children: Snippet;
        secondChild: Snippet;
        name: string;
        fake_name ?: string | null;
    } = $props();
</script>
<!--HTML-->
<!--Runes: with $ - are important-->

<!--<h1>Hello {name}</h1>-->
<!--<h2>{name.replaceAll('a', 'X')}</h2>-->
<!--{fake_name}-->

<div>
    <h1>
        {name ? name : 'No name'}'s Form
    </h1>
    <!--{@render children()}-->
    <!--<h3>{@render secondChild()}</h3>-->

</div>


<!--CSS-->
<style>
    /*div{*/
    /*    background: yellow;*/
    /*}*/
    h1 {
        color: red;
    }
</style>