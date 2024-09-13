<template>
  <div id="app">
    <div class="container">
      <!-- Click Counter -->
      <section class="section click-counter">
        <h2>Click Counter</h2>
        <button @click="clickCount++" class="button">Click Me!</button>
        <p class="count-text">Button clicked {{ clickCount }} times.</p>
      </section>

      <!-- Color Changer -->
      <section class="section color-changer">
        <h2>Color Changer</h2>
        <button @click="changeColor" class="button">Change Background Color</button>
        <div class="color-box" :style="{ backgroundColor: currentColor }"></div>
      </section>

      <!-- Image Carousel -->
      <section class="section image-carousel">
        <h2>Image Carousel</h2>
        <div class="carousel-container">
          <div class="carousel-images" :style="{ transform: 'translateX(' + (-currentIndex * 300) + 'px)' }">
            <img v-for="(image, index) in images" :key="index" :src="image" alt="Image">
          </div>
          <button @click="prevImage" class="carousel-button">Previous</button>
          <button @click="nextImage" class="carousel-button">Next</button>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      clickCount: 0,
      currentColor: '#ffffff',
      colors: ['#ff9999', '#99ff99', '#9999ff', '#ffff99'],
      currentIndex: 0,
      images: [
        'https://picsum.photos/300/200?random=1',
        'https://picsum.photos/300/200?random=2',
        'https://picsum.photos/300/200?random=3'
      ]
    };
  },
  methods: {
    changeColor() {
      const randomIndex = Math.floor(Math.random() * this.colors.length);
      this.currentColor = this.colors[randomIndex];
    },
    prevImage() {
      this.currentIndex = (this.currentIndex === 0) ? this.images.length - 1 : this.currentIndex - 1;
    },
    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.section {
  margin-bottom: 40px;
}

h2 {
  font-size: 1.5em;
  margin-bottom: 10px;
}

.button {
  padding: 10px 20px;
  font-size: 1em;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.button:hover {
  background-color: #0056b3;
}

.count-text {
  font-size: 1.2em;
  margin-top: 10px;
}

.color-box {
  height: 100px;
  width: 100%;
  border: 1px solid #ddd;
  margin-top: 10px;
}

.carousel-container {
  position: relative;
  width: 300px;
  overflow: hidden;
  margin: 0 auto;
}

.carousel-images {
  display: flex;
  transition: transform 0.5s ease;
}

.carousel-images img {
  width: 300px;
  height: 200px;
  object-fit: cover;
}

.carousel-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: 10px;
  font-size: 1em;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.carousel-button:hover {
  background-color: #0056b3;
}

.carousel-button:first-of-type {
  left: 10px;
}

.carousel-button:last-of-type {
  right: 10px;
}
</style>
