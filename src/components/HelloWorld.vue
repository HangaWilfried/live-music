<template>
  <input type="text" v-model.trim="star">
  <button @click.prevent="displayData">search</button>

  <div>
    <div v-for="(song, index) in songs.slice(0, 10)" :key="index">
        <div>name-{{song.artistName}}</div>
        <div>- <img :src="song.artworkUrl60"></div>
        <div>Prix ${{song.collectionPrice}}</div>
        <div>audio- <audio :src="song.collectionViewUrl" controls></audio></div>
        <div>video-
          <video :src="song.previewUrl" controls></video>
        </div>
        <div>Title-{{song.trackCensoredName}}</div>
    </div>
  </div>

</template>

<script>
  import { ref, reactive } from 'vue'
  import axios from 'axios'
  export default {
    name: 'HelloWorld',
    setup(){
      const star = ref('')  
      let songs = reactive([])
  
      
      async function displayData(){
        songs.length = 0
        const {data:{results}} = await axios.get(`https://itunes.apple.com/search?term=${star.value}&limit=25&entity=musicVideo`)
        console.log(results);
        songs.push(...results)
      }
    return{ 
      star, displayData, songs
    }
  }
}
</script>

