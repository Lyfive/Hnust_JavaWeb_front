<script>

</script>

<template>
    <div class="box">
        <div class="home">
            <div class="line">
                <div class="row"></div>
                <div class="row"></div>
                <div class="row"></div>
            </div>
            <div class="line">
                <div class="row"></div>
                <div class="row"></div>
                <div class="row"></div>
            </div>
            <div class="line">
                <div class="row"></div>
                <div class="row"></div>
                <div class="row"></div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.box {
    position: absolute;
    top: 1rem;
    left: 4rem;
    height: 95%;
    width: 90%;
    background-color: #fff;
    box-shadow: -0.1rem -0.1rem 0.1rem rgb(253, 240, 196);
}

.home {
    display: grid;
    width: 100%;
    height: 100%;
}

.line {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 10%;
    background-color: #111;
    
}

.row {
    display: grid;
    grid-template-rows: 1fr;
    margin-right: 2rem;
    background-color: pink;
}
</style>