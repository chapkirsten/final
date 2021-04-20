<template>
<div>
  <section class="image-gallery">
    <div class="image" v-for="photo in photos" v-bind:key="photo._id">
      <img :src="photo.path" />
      <br/>
      <p class="photoTitle"><strong>{{photo.title}}</strong></p>
      <hr/>
      <p class="description">{{photo.description}}</p>
      <hr/>
      <p class="reviewer"><strong>Reviewer: </strong></p>
      <p class="photoName">{{photo.user.firstName}} {{photo.user.lastName}}</p>
      <p class="photoDate">{{formatDate(photo.created)}}</p>
      <br/>



    </div>
  </section>
</div>
</template>


<script>
import moment from 'moment';
export default {
  name: 'ImageGallery',
  components: {
  },
  data() {
    return {
      show: false,
    }
  },
  props: {
    photos: Array
  },
  methods: {
    formatDate(date) {
      if (moment(date).diff(Date.now(), 'days') < 15)
        return moment(date).fromNow();
      else
        return moment(date).format('d MMMM YYYY');
    },
    showreview(){
      this.show = true;
    },
    close(){
      this.show = false;
    },
    async reviewFinished() {
      this.show = false;
    },
  }
}
</script>


<style scoped>

.description{
  text-align: center;
}
button{
  background-color: #BF5B04;
  margin: 0 auto;
  display: block;
}
.reviewer{
  text-align: center;
  font-family: georgia;
}
.photoTitle{
  font-size: 20px;
  text-align: center;
  font-family: georgia;
}
.photoName{
  text-align: center;
  font-size: 15px;
}
.photoInfo {
  display: flex;
  justify-content: space-between;
  font-size: 0.8em;
}
.photoInfo p {
  margin: 0px;
}
.photoDate {
  font-size: 0.7em;
  font-weight: normal;
  text-align: center;
}
p {
  margin: 0px;
}
/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}
.image-gallery {
  column-gap: 10em;
}
.image {
  margin: 0 0 1.5em;
  display: inline-block;
  outline-style: double;
  margin-top: 200px;
  width: 150%;
}
.image img {
  width: 100%;
}


/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 4;
  }
}
/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
}
/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
}
</style>
