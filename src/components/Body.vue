<template>
    <div>
        <div class="col-md-12">
        <h1>Quote Added</h1>
        <div id="progress-bar">
            <div id="progress" :style="{'width':width+'%'}"><div class="text-center">{{numb}}/100</div>
            </div>
        </div>
        </div><br><br>
        <div class="row">
        <div class="col-md-6 col-md-offset-3 col-sm-8 col-sm-offset-2 col-xs-10 col-xs-offset-1">
            <h5>Quote</h5>
            <div class="form-group">
            <textarea class="form-control" rows="3" v-model="value"></textarea>
            </div>
            <div class="text-center"><button class="btn btn-info" @click="add">Add Quote</button></div>
        </div><hr>
        </div>
        <div class="row">
     <div class="col-md-3" id="quote" @click="remove" v-for="quote in quotes" :key="quote"><div id="quote-inner">{{quote}}</div></div>
    </div>
    <div class="col-md-12 bg-info text-center" id="info">Info: Click on the Quote to delete it</div>
    </div>
</template>
<script>
export default {
    data: function(){
        return {
            quotes: [],
            value: '',
            width: 0,
            numb: 0
        }
    },
    methods: {
        add: function(){
            if (this.quotes.length <=9 ) {
                if(this.value !== ''){
             this.quotes.unshift(this.value);
             this.value = '';
             this.width += 10;
             var i = 0;
             var vm = this;
             var timerId = setInterval(function(){
                 i++ ;
                vm.numb = (vm.numb) +i;
                i=0;
             },100)
             setTimeout(function(){
                clearInterval(timerId);
                },1000);
            }
            }  
        },
        remove: function(e){
            this.width -= 10;
             var i = 0;
             var vm = this;
             var timerId2 = setInterval(function(){
                 i++ ;
                vm.numb = (vm.numb) -i;
                i=0;
             },100)
             setTimeout(function(){
                clearInterval(timerId2);
                },1000);
            for(var q=0;q<this.quotes.length;q++){
                if (this.quotes[q] === e.target.innerText) {
                    return this.quotes.splice(q,1)
                }
            }
        }
    }
}
</script>
<style scoped>
    #progress-bar{
        width: 100%;
        height: 1.2em;
        /* box-shadow: -2px -2px 3px #ccc; */
        background-color: #eae5e5;
        border: 1px solid #ccc;
        border-radius: 7px;
    }
    #progress{
        width: 70%;
        height: 100%;
        color: white;
        /* box-shadow: -2px -2px 3px #ccc; */
        background-color: #17a2b8;
        border-radius: 7px;
        transition: width 1s;
    }
    #quote{
        text-align: center;
        font-size: 120%;
        font-style: italic;
        display: inline-block;
        
    }
    #quote-inner{
        border-radius: 7px;
        border: 1px solid #ccc;
        width: 100%;
        height: 4em;
        padding: 1em;
        margin-top: 1em;
        margin-bottom: 1em;
        cursor: pointer;
        overflow-wrap: break-word;
        overflow-y: auto;
    }
    #quote-inner:hover{
        background-color: aqua;
        width: 110%;
        height: 4.2em;
    }
    #info{
        padding: 1em;
        border-radius: 7px;
    }
</style>


</style>
