<template>
    <date-picker :date="date" />
</template>

<script>
import datePicker from './DatePicker'
export default {
    components:{
        datePicker,
    },
    data(){
        return {
            date:new Date(),
        }
    }
}
</script>
<style scoped>

</style>