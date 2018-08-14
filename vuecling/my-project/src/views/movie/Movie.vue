<template>
    <div>
        <div class="container">
            <h1>电影</h1>
            <ul>
                <li v-for="(items,index) in dataList" :key='index+"dl"'>

                    <img :src="items.images.small" alt=""> {{items.title}}
                </li>
            </ul>
        </div>

        <div class="loading" v-show="!isFinish">
            <div class="load-content">
                <img src="@/assets/loading.gif" alt="">
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        created() {
            this.getData()
        },
        data () {
            return {
                dataList:[],
                isFinish:true
            }
        },
        mounted(){
            window.onscroll=()=>{
                console.log(document.documentElement.scrollTop);
                console.log('可视高度'+document.documentElement.clientHeight);
                console.log('滚动高度'+document.documentElement.scrollHeight);
                let sTop = document.documentElement.scrollTop;
                let sHeigth = document.documentElement.scrollHeight;
                let cHeight = document.documentElement.clientHeight;
                if(sTop+cHeight==sHeigth){
                    console.log('end');
                    if(this.isFinish==true){
                        this.getData();
                    }

                }
            }
        },
        methods:{
            getData(){
                this.isFinish=false;
                // axios.get(API_PROXY+'https://api.douban.com/v2/movie/in_theaters')
                axios.get('https://api.myjson.com/bins/nsb9g')
                    .then((response)=>{

                        this.dataList=this.dataList.concat(response.data.subjects)
                        console.log(response);
                        this.isFinish=true;

                    })
                    .catch((error)=>{
                        console.log(error);
                    })
            },
        }



    }

</script>
<style scoped>


    ul li img{
        width: 50%;
    }
.loading{
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background: rgba(0,0,0,.5);

}
.load-content{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    padding: 1rem;
    border-radius: .1rem;
    background: rgba(255,255,255)
}

</style>
