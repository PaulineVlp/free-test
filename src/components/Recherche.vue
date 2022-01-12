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
            class="my-2 my-sm-0"
            @click="$bvModal.show('display-film')"
            variant="primary"
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

          <!-- Pop-up qui affiche les détails du film hide-footer -->
          <b-modal id="display-film" centered>
            <template #modal-title>
              <b>{{ getFilm() }}</b>
            </template>

            <div class="d-block" v-if="film_actif">
              <b-row>
                <b-col v-if="film_actif.Poster !== 'N/A'">
                  <b-img :src="getPoster()" fluid alt="Poster"></b-img>
                </b-col>
                <b-col>
                  <p>
                    <span><b>Directeur: </b>{{ film_actif.Director }}</span>
                    <br /><br />
                    <span><b>Intrigue: </b>{{ film_actif.Plot }}</span>
                  </p>
                </b-col>
              </b-row>
            </div>

            <template #modal-footer>
              <b-button
                variant="dark"
                class="float-right"
                @click="$bvModal.hide('display-film')"
              >
                Fermer
              </b-button>
            </template>
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
    film_actif: "",
  }),
  methods: {
    getListFilms() { // recup liste des films de l'API
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
    getFilm() { // recup données du film correspondant à ce qui a été rentré (query)
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
    getPoster() { // retourne le lien de l'affiche du film
      return this.film_actif.Poster;
    },
  },
  mounted() {
    this.getListFilms();
  },
};
</script>

<style scoped>

</style>
