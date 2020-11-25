<template>
    <div 
    class="date-picker"
    v-click-outside
    >
        <div class="picker-input">
            <span class="input-prefix">
                <i class="iconfont icon-date"></i>
            </span>
            <input type="text" :value="chooseDate">
        </div>

        <div 
        class="picker-panel"
        v-if="showPicker"
        >
            <div class="picker-arrow" />
            <div class="picker-body">
                <div class="picker-header">
                    <span class="pre-year iconfont icon-pre-year"/>
                    <span class="pre-month iconfont icon-pre-month" />
                    <span class="picker-date">2020年11月</span>
                    <span class="next-month iconfont icon-next-month" />
                    <span class="next-year iconfont icon-next-year" />
                </div>

                <div class="picker-content">
                    <div class="picker-weeks">
                        <div 
                        v-for="week in weeks"
                        :key="week">{{ week }}</div>
                    </div>
                <div class="picker-day">
                    <div
                        :class="{active:isActive}"
                        v-for="day in 42"
                        :key="day"
                        >{{ day }}</div>
                    </div>
                </div>
            </div>
            
        </div>
    </div>
</template>

<script>
export default {
    props:{
        date:{
            type:Date,
            default:()=>new Date(),
        }
    },
    directives:{
        "click-outside":{
            bind(el,binding,vnode){
                const vm = vnode.context;
                document.onclick = e=>{
                    const isElson = el.contains(e.target);
                    if(isElson && !vm.showPicker){
                        vm.changeShow(true);
                    }else if(!isElson && vm.showPicker){
                        vm.changeShow(false)
                    }
                    
                }
                
            }
        }
    },
    data(){
        return {
            weeks:["日","一","二","三","四","五","六"],
            isActive:false,
            showPicker:false,
        }
    },
    computed:{
        chooseDate(){
            const year = this.date.getFullYear();
            const month = this.date.getMonth();
            const day = this.date.getDay();
            return `${year}-${month+1}-${day}`
        }
    },
    methods:{
        changeShow(flag){
            this.showPicker = flag;
        }
    }
}
</script>

<style scoped>
@import "./asset/font.css";
.picker-input{
    width: 250px;
    height: 40px;
    position: relative;
}
.date-picker{
    display: inline-block;
}
.picker-input input{
    width: 100%;
    height: 40px;
    line-height: 40px;
    outline: none;
    padding-left: 50px;
    box-sizing: border-box;
    border-radius: 5px;
    border: 1px solid rgb(177, 174, 174);
}
.input-prefix{
    position: absolute;
    left: 10px;
    z-index: 2;
    top: 50%;
    transform: translateY(-50%);
}

.picker-arrow{
    width: 0;
    height:0;
    border: 10px solid transparent;
    border-bottom-color: #ccc;
    position: relative;
    left: 58px;
    top: -21px;
}
.picker-arrow::after{
    content: "";
    position:absolute;
    left: -9px;
    top: -6px;
    width: 0;
    height:0;
    border: 9px solid transparent;
    border-bottom-color: #fff;
}
.picker-panel{
    border: 1px solid #ccc;
    border-radius: 10px;
    box-shadow: 2px 2px 4px #ccc;
    margin-top: 10px;
    display: inline-block;
    background: #fff;
    position: absolute;
}

.picker-header{
    padding: 0 40px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 50px;
}
.picker-header .picker-date{
    margin: 0 50px;
}
.picker-header span:not(.picker-date){
    cursor: pointer;
    width: 30px;
}
.picker-content .picker-weeks{
    display: flex;
    justify-content: space-around;
    margin: 0 20px;
    padding-bottom: 10px;
    border-bottom: 1px solid rgba(214, 214, 214, 0.712);
}
.picker-content .picker-weeks div{
    text-align: center;
    width: 30px;
    height: 30px;
}
.picker-content .picker-day{
    display: flex;
    flex-wrap: wrap;
    margin: 20px 20px;
    width: 350px;
    justify-content: start;
}
.picker-content .picker-day div{
    text-align: center;
    width: 50px;
    height: 50px;
    line-height: 50px;
    color: rgb(138, 135, 135);
    cursor: pointer;
    user-select: none;
}
.picker-content .picker-day div:hover{
    color: rgb(0, 195, 255);
}
.active{
    background-color: rgb(8, 142, 231);
    border-radius: 50%;
    color: #fff !important;
}
</style>