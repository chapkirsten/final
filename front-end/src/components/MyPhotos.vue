<template>
<div class="main">
  <p class="log">{{user.firstName}} {{user.lastName}} <a @click="logout"><i class="fas fa-sign-out-alt"></i></a></p>
  <p class="col">Add your book review<a @click="toggleUpload"><i class="fas fa-image"></i></a></p>
  <uploader :show="show" @close="close" @uploadFinished="uploadFinished" />

  <div class="heading">
     <h2>Edit/Delete an Item</h2>
   </div>
   <div class="edit">
     <div class="form">
       <input v-model="findTitle" placeholder="Search">
       <div class="suggestions" v-if="suggestions.length > 0">
         <div class="suggestion" v-for="s in suggestions" :key="s.id" @click="selectItem(s)">{{s.title}}
         </div>
       </div>
     </div>
     <div class="upload" v-if="findItem">
       <input v-model="findItem.title">
       <p></p>
       <img :src="findItem.path" height="200px;"/>
     </div>
     <div class="actions" v-if="findItem">
       <button @click="deleteItem(findItem)">Delete</button>
       <button @click="editItem(findItem)">Edit</button>
     </div>
     <br/>
     <br/>
   </div>



  <image-gallery :photos="photos" />
  <p v-if="error">{{error}}</p>
</div>
</template>



<script>
import axios from 'axios';
import Uploader from '@/components/Uploader.vue';
import ImageGallery from '@/components/ImageGallery.vue';
export default {
  name: 'MyPhotos',
  components: {
    Uploader,
    ImageGallery
  },
  data() {
    return {
      show: false,
      photos: [],
      error: '',
      items: [],
      findTitle: "",
      findItem: null,
    }
  },
  created() {
    this.getItems();
  },
  computed: {
    user() {
      return this.$root.$data.user;
    },
    suggestions() {
      let items = this.items.filter(item => item.title.toLowerCase().startsWith(this.findTitle.toLowerCase()));
      return items.sort((a, b) => a.title > b.title);
    },

  },
  methods: {
    async logout() {
      try {
        await axios.delete("/api/users");
        this.$root.$data.user = null;
      } catch (error) {
        this.$root.$data.user = null;
      }
    },
    async getItems() {
      try {
        let response = await axios.get("/api/photos");
        this.items = response.data;
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    async deleteItem(photo) {
      try {
        await axios.delete("/api/photos/" + photo._id);
        this.findItem = null;
        this.getItems();
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    async editItem(photo){
      try {
        await axios.put("/api/photos/" + photo._id, {
          description: this.findItem.description,
        });
        this.findItem = null;
        this.getItems();
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    close() {
      this.show = false;
    },
    toggleUpload() {
      this.show = true;
    },
    async uploadFinished() {
      this.show = false;
      this.getPhotos();
    },
    selectItem(item) {
      this.findTitle = "";
      this.findItem = item;
    },
  }
}
</script>


<style scoped>

.menu h2 {
  font-size: 14px;
}
.log{
  margin-top: 200px;
}
.col{
  margin-top: 10px;
}
.fas{
  color: #BF5B04;
}
</style>
