<template>
  <div id="app">
    <input v-model="mail" placeholder="example@mail.com" :maxlength="100" :disabled="dateNaissanceValid==false || telephoneValid==false"/>
    <span v-if="this.mailValid==false">Le mail saisie n'est pas valide</span>
    <br>
    <input v-model="prenom" placeholder="prenom" :maxlength="tailleMax"/>
    <br>
    <input v-model="nom" placeholder="nom" :maxlength="tailleMax"/>
    <br>
    <input type="radio" id="Masc" value="true" v-model="sexe">
    <label for="Masc">Masculin</label>
    <input type="radio" id="Fem" value="false" v-model="sexe">
    <label for="Fem">Feminin</label>
    <br>
    <input v-model="telephone" placeholder="0612345678" :maxlength="tailleMax" :disabled="dateNaissanceValid==false || mailValid==false"/>
    <span v-if="this.telephoneValid==false">Le numero saisie n'est pas valide</span>
    <br>
    <input v-model="dateNaissance" placeholder="01/01/1990" :maxlength="tailleMax" :disabled="mailValid==false || telephoneValid==false"/>
    <span v-if="this.dateNaissanceValid==false">Le date saisie n'est pas valide</span>
    <br>
    <button v-on:click="sendData" :disabled="mailValid==false ||telephoneValid==false ||dateNaissanceValid==false">Valider</button>
  </div>
</template>


<script>
export default {
  name: 'Inscription',
  data : function(){
    return {
        mail:'',
        telephone:'',
        nom:'',
        prenom:'',
        dateNaissance:'',
        sexe:null,
        tailleMax:15,
        mailValid:true,
        telephoneValid:true,
        dateNaissanceValid:true,
      }
    },
    watch: {
        mail: function() {
            var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            this.mailValid= re.test(this.mail);
            
        },
        telephone: function() {
            var re = /^(0|\+33)[1-9]([-. ]?[0-9]{2}){4}$/;
            this.telephoneValid = re.test(this.telephone)
        },
        dateNaissance: function() {
            var re = /^(0[1-9]|[12][0-9]|3[01])[- /.](0[1-9]|1[012])[- /.](19|20)\d\d$/;
            this.dateNaissanceValid = re.test(this.dateNaissance)
        }
    },
    methods: {
    sendData: function () {
      alert("Le formulaire a bien ete enregistre")
      location.reload()
    }
  }

}
</script>


