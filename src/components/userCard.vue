<template>
   <div class="d-flex justify-content-between mb-2">
        <div class="ml-3">{{ user.name }}</div>
        <div class="ml-auto">{{ formatNumberMMK(user.income) }}</div>
    </div>                            
</template>

<script>
export default {
    name: "userCard",
    //data passing throuth partent to child
    //child accept 
    //can send object or data or function
    props: ['user', "formatNumberMMK"]
};
</script>

<style>

</style>