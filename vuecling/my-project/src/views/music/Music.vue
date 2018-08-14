<template>
    <div>
        <div class="container">
            <ul>
                <li v-for="(items,index) in dataList" :key='index+"dl"' @click="$router.push('/test1/music')">
                    <img :src="'../' + items.bg"/>
                </li>
            </ul>
            <router-view/>
        </div>

    </div>

</template>
<script>

    import axios from 'axios'
    export default {
        data(){
            return {
                dataList:[]
            }
        },
        created(){
            this.getData()
        },
        methods:{
            getData(){
                axios.get('../data/musiclist.json')
                    .then((response)=>{
                        console.log(response);
                        this.dataList=response.data.albums
                    })
                    .catch((error)=>{
                        console.log(error);
                    })
            }
        }
    }

</script>
<style scoped>
ul li {
    width: 50%;
    float: left;
}
ul li img{
    width: 100%;
}

</style>
