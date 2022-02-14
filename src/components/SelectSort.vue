<template>
    <select class="select-sort">
        <option default>От меньшего к большему</option>
        <option>От большего к меньшему</option>
        <option>По наименованию</option>
    </select>
</template>

<script>
export default {

}
</script>

<style scoped>
    .select-sort {
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        padding: 10px 16px;
        border: none;
        outline: none;
        cursor: pointer;

        /* style for text */
        font-weight: normal;
        font-size: 12px;
        color: #B4B4B4;
    }
</style>