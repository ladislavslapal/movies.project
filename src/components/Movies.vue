<template>
  <div class="search">
    <input type="text" class="searchTerm" v-model="search" placeholder="vyhledat film pomocí názvu" />
  </div> <br>
  <button @click="toggleShowMovies" class="btn">
    <span v-if="showMovies">skrýt seznam filmů</span>
    <span v-else>zobrazit seznam filmů</span>
  </button>
  <div v-if="showMovies">
  <div class="movie" v-for="movie in searchBar" :key="movie.value"  :class="{ fav: movie.isFav }">
    <h1 contenteditable>{{movie.name}}</h1>
    <p>Release Date: {{movie.year}}</p>
    <p contenteditable>Watch Time: {{movie.runtime}}</p>
    <p contenteditable>Genre: {{movie.categories}}</p>
    <p contenteditable>Director: {{movie.director}}</p>
    <p contenteditable>{{movie.storyline}}</p>
    <button @click="toggleMarkFavorite(movie)" class="movbutton">
      <span v-if="!movie.isFav">Přidat do oblíbených</span>
      <span v-else>Odebrat z oblíbených</span>
    </button>
  </div>
  </div>


</template>

<script>

export default {
  name: "Movies",
  components: {  },
  data() {
    return {
      showMovies: true,
      isFav: false,
      Movies: [],
      search: "",
    }
  },

  methods: {
    toggleShowMovies() {
      this.showMovies = !this.showMovies
    },

    toggleMarkFavorite(movie) {
      movie.isFav = !movie.isFav
    },
  },

  computed: {
    searchBar() {
      return this.Movies.filter(p => {
        // return true if the product should be visible

        // in this example we just check if the search string
        // is a substring of the product name (case insensitive)
        return p.name.toLowerCase().indexOf(this.search.toLowerCase()) != -1;
      });
    }
  },


  mounted() {
    fetch('http://localhost:3000/Movies')
        .then((res) => res.json())
        .then(data => this.Movies = data)
        .catch(err => console.log(err.message))
  }
}
</script>

<style scoped>

.movbutton {
  color: #00B4CC !important;
}

.search {
  width: 100%;
  position: relative;
  display: flex;
  width: 20%;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);

}

.searchTerm {
  width: 100%;
  border: 3px solid white;
  padding: 5px;
  height: 20px;
  border-radius: 5px;
  outline: none;
  color: #9DBFAF;
}

.searchTerm:focus{
  color: #00B4CC;
}

div.fav {
  background: #FEC2D6;
}

button {
  background: none;
  border: 0;
  box-sizing: border-box;
  margin: 1em;
  padding: 1em 2em;
  box-shadow: inset 0 0 0 2px white;
  color: white !important;
  font-size: inherit;
  font-weight: 700;
  position: relative;
  vertical-align: middle;
}

button::before,
button::after {
   box-sizing: inherit;
   content: '';
   position: absolute;
   width: 100%;
   height: 100%;
 }

button:hover {
   color: #00B4CC;
 }

button::before,
button::after {
   top: 0;
   left: 0;
   height: 100%;
   width: 100%;
   transform-origin: center;
 }

button::before {
   border-top: 2px solid #00B4CC;
   border-bottom: 2px solid #00B4CC;
   transform: scale3d(0,1,1);
 }

button::after {
   border-left: 2px solid #00B4CC;
   border-right: 2px solid #00B4CC;
   transform: scale3d(1,0,1);
 }

button:hover::before,
button:hover::after {
   transform: scale3d(1,1,1);
 transition: transform 0.5s;
 }



.movie {
  width: 400px;
  padding: 20px;
  margin: 100px auto;
  background: rgb(222, 222, 222);
  border-radius: 20px;
}

.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0,0,0,0.5);
  width: 100%;
  height: 100%;
}
.movie h1 {
  color: deepskyblue;
  border: none;
  padding: 0;
}

.movie p {
  font-style: normal;
}
.movie .actions {
  text-align: center;
  margin: 30px 0 10px 0;
}
.movie .actions a {
  color: #333;
  padding: 8px;
  border: 1px solid #eee;
  border-radius: 4px;
  text-decoration: none;
  margin: 10px;
}

.movie.sale {
  background: crimson;
  color: white;
}
.movie.sale h1 {
  color: white;
}
.movie.sale .actions {
  color: white;
}
.movie.sale .actions a {
  color: white;
}

</style>