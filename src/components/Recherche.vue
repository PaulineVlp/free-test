<template>
  <div class="Recherche">
    <b-container fluid>
      <b-row align-h="center">
        <b-col cols="4">
          <!-- Barre de recherche + bouton qui ouvre un pop-up -->
          <b-form-input
            v-model="query"
            list="liste_films_id"
            placeholder="Rechercher un film"
          ></b-form-input>
          <br />
          <b-button
            size="sm"
            class="my-2 my-sm-0"
            @click="$bvModal.show('display-film')"
            variant="info"
            >Recherche</b-button
          >

          <!-- Réduit le champ des possibles selon ce qui est tapé dans la barre -->
          <b-form-datalist
            id="liste_films_id"
            :options="
              liste_films.map(function (e) {
                return { text: e.Title + ', ' + e.Year + ' ' };
              })
            "
          >
          </b-form-datalist>

          <!-- Pop-up qui affiche les détails du film -->
          <b-modal id="display-film" hide-footer>
            <template #modal-title>
              {{ getFilm() }}
            </template>
            <div class="d-block text-center" v-if="film_actif">
              <h3>Hello From This Modal!</h3>
            </div>
            <b-button class="mt-3" block @click="$bvModal.hide('display-film')"
              >Fermer</b-button
            >
          </b-modal>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Recherche",
  data: () => ({
    liste_films: [],
    query: "",
    query_temp: "",
    film_actif: "",
  }),
  methods: {
    getListFilms() {
      const options = {
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
      };
      this.axios
        .get(
          "http://www.omdbapi.com/?apikey=9ddde0b3&type=movie&s=%5Btitre%5D%60",
          options
        )
        .then((response) => {
          this.liste_films = response.data.Search;
        });
    },
    getFilm() {
      var splitted = this.query.split(", ", 2);
      this.film_actif = this.liste_films.find(
        (film) => film.Title === splitted[0] && film.Year === splitted[1]
      );
      if (this.film_actif) {
        return this.film_actif.Title;
      } else {
        return "Pas de film sélectionné";
      }
    },
  },
  mounted() {
    this.getListFilms();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
