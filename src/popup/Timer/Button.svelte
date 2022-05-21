<script>
    export let text, bgColor;
</script>

<main>
    <button style="background-color: {bgColor}" on:click >{text}</button>
</main>

<style>
    button {
        padding: 10px 15px;
        border: none;
        border-radius: 4px;
        color: #fff;
        font-weight: 600;
        font-size: 25px;
        font-family: 'Bitter', serif;
        cursor: pointer;
    }
</style>