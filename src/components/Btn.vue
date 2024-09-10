<script>
export default{
    
    data() {
        return{
            
        };
    },

    methods: {
        
    },
}
</script>

<template>
    <div class="btn"><slot /></div>
</template>

<style scoped>
.btn{
    background-color:rgb(17, 154, 17);
    width:100px;
    height:50px;
    border-radius: 8px;
    color: black;
    cursor: pointer;
    text-align: center;
    line-height: 50px;
    margin-left: 10px;
    margin-right: 10px;
}

.btn:hover{
    background-color:rgb(206, 151, 32);
}
</style>