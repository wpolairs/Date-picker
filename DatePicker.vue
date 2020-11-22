<template>
    <div class="date-picker">
        <div class="picker-input">
            <span class="input-prefix">
                <i></i>
            </span>
            <input type="text">
        </div>

        <div class="picker-panel">
            <div class="picker-arrow" />
            <div class="picker-body">
                <div class="picker-header">
                    <span class="pre-year" />
                    <span class="pre-month" />
                    <span class="picker-date"></span>
                    <span class="next-month" />
                    <span class="next-year" />
                </div>

                <div class="picker-content">
                    <div 
                    class="picker-weeks"
                    v-for="week in weeks"
                    :key="week"
                    >{{ week }}</div>

                    <div 
                    class="picker-day"
                    v-for="day in 42"
                    :key="day"
                    >{{ day }}</div>
                </div>
            </div>
            
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            weeks:["日","一","二","三","四","五","六"]
        }
    }
}
</script>

<style scoped>

</style>