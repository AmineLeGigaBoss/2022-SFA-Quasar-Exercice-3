<template>
  <!--
Exercice 3 - Vuex & Formulaires

1) Créer un magasin, module, Vuex avec le namespace "taches" pour les plats
   dans src/store/ et y ajouter le tableau des plats.

2) Créer un getter pour récupérer les plats
   et afficher ces derniers sur la page ExercicePage.vue à l'aide du getter

3) Ajouter la possibilité de supprimer un élément (clic sur bouton supprimer)
   en utilisant des actions et des mutations.
   Afficher une dialog de confirmation avant de supprimer.

4) Ajouter une validation au formulaire src/components/FormPlat.vue
     - nom: obligatoire avec un maximum de 20 caractères.
     - description: maximum de 155 caractères.
     - La validation doit être déclenchée lorsque l'on clique sur Sauvegarder

5) Ajouter la possibilité d'ajouter un élément
   indice: utiliser l'attribut "action" pour différencier l'ajout de la modification

6) Ajouter la possibilité de modifier un élément

7) Si aucune description n'est fournie pour un plat,
   afficher le texte "Aucune description fournie" en italique

8) Si aucune image n'est fournie, utiliser l'image statics/image-placeholder.png

-->
  <q-page class="q-pa-lg">
    <div class="row q-gutter-lg">

      <plat
        v-for="plat in plats"
        :key="plat.id"
        :plat="plat" />

      <bouton-ajouter
        @click="afficherFormPlat = true" />

      <q-dialog
        v-model="afficherFormPlat">

        <form-plat
          @close="afficherFormPlat = false"
          action="ajouter" />
      </q-dialog>

    </div>
  </q-page>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  data () {
    return {
      afficherFormPlat: false
    }
  },
  components: {
    plat: require('components/PlatVue.vue').default,
    'bouton-ajouter': require('components/BoutonAjouter.vue').default,
    'form-plat': require('components/FormPlat.vue').default
  },
  computed: {
    // plats () {return this.$store.getters['plats/plats']}
    ...mapGetters('plats', ['plats'])
  }
}
</script>
