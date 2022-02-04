<template>
    <div class="hobbies">
        <span v-for="el in likes" :key="el">
            {{el}}
        </span>
    </div>
</template>

<script>
export default {
    name : 'Hobbies',
    props : {
        likes : {
            require : true,
            type : Array,
        }
    }
}
</script>

<style lang="scss" scoped>
.hobbies{
    display: grid;
    grid-template-columns:1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    width: 100%;
    margin-top:1rem;
    gap:.4rem;
    span{
        font-family: Poppins;
        background: #FFFFFF;
        font-size:.5rem;
        height: 2rem;
        text-align: center;
        /* #BFC8E6 */
        border: 1px solid #BFC8E6;
        border-radius: 10px;
        color:#849FFF;
        font-size:.8rem;
        padding:.2rem .5rem;
        }
    }
</style>