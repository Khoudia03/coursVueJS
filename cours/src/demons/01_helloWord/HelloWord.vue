
<script setup>
    const message = "Naruto Uzumaki!";
</script>


<template>
        <section class="card">

            <h2>01_Hello Word</h2>
            <p>Premier Composant vue (SFC)</p>
            <div class="box">
                <strong>Message:</strong>{{ message.toUpperCase() }}
            </div>

        </section>
</template>


<style>
.card
{
    background-color: blanchedalmond;
    padding: 16px;
    border: 1px solid #eee;
    border-radius: 12px;
}
.box
{
    margin-top: 10px;
    padding: 12px;
    border: 1px dashed #ccc;
    border-radius: 10px;
}
</style>