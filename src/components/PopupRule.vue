<template>
    <div class="wrapper-popup" v-bind:class="{up : true ?guideUp ==1 : false }">
        <div class="rule">
            <h3>Luật chơi</h3>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ad at amet, eos ex ratione aperiam dolores quo iure dignissimos consequatur quam maxime esse laudantium hic sunt, laborum ducimus, nesciunt natus!</p>
            <button v-on:click = "backGuide">Đã hiểu</button>
        </div>
        
    </div>
</template>

<script>
export default {
    name: 'popupRule',
    data() {
        return {

        }
    },
    props: {
        guideUp: Number
    },
    methods: {
        backGuide(){
            this.$emit('backGuide')
        }
    }
}
</script>

<style>
    .wrapper-popup {
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        background-color: rgba(0,0,0,0.4);
        opacity: 0;
        visibility: hidden;
    }
    .up{
        opacity: 1;
        visibility: inherit;
    }
    .rule{
        width: 350px;
        top: 50%;
        left: 50%;
        padding: 20px;
        transform: translate(-50%, -50%);
        position: absolute;
        background-color: #fff;
        border-radius: 5px;
        border: 2px solid #ccc;
    }
    .rule button {
        margin-top: 16px;
        padding: 8px;
        font-weight: 600;
        background-color: rgb(73, 233, 121);
    }
    .rule button:hover{
        cursor: pointer;
        background-color: rgb(147, 182, 154);
    }
    .rule h3{
        font-size: 50px;
        font-weight: 700;
    }
</style>