<script setup>
    const image = "https://i.pinimg.com/736x/fb/2f/b7/fb2fb70e3d0e876e5d20575088967cd7.jpg"
    const boutton = false;
</script>


<template>
    <section>
        <img :src="image">
        <button :disabled="boutton">Clique Me</button>
    </section>
</template>



<style>

</style>