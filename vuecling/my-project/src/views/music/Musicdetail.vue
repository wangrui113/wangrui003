<template>
    <div class="song">
       <!-- <aplayer autoplay
                 :music="{
                title: 'secret base~君がくれたもの~',
            artist: 'Silent Siren',
            src: 'https://moeplayer.b0.upaiyun.com/aplayer/secretbase.mp3',
            pic: 'https://moeplayer.b0.upaiyun.com/aplayer/secretbase.jpg'
        }"
        />
-->

       <aplayer v-if="isIf" :list="dataList" :music="dataList[0]" :showlrc="true"/>

    </div>
</template>

<script>
    import Aplayer from 'vue-aplayer'
    import axios from 'axios'
    export default {
        name: "musicdetail",
        components: {
            Aplayer
        },
        data(){
            return {
                dataList:[],
                isIf:false
            }
        },
        created(){
            this.getData()
        },
        methods:{
            getData(){
                axios.get('../data/musicdata.json')
                    .then((response)=>{
                        console.log(response);
                        this.dataList=response.data.musicData;
                        console.log(this.dataList)
                        this.isIf=true;
                        console.log(123)
                        for(var i=0 ;i<response.data.musicData.length;i++){
                            this.dataList[i].lrc = 'http://localhost:8080/'+response.data.musicData[i].lrc;
                        }
                    })
                    .catch((error)=>{
                        console.log(error);
                    })
            }
        }
    }


</script>

<style scoped>

</style>