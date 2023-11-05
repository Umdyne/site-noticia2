<template>
  <v-app class="bg-grey-darken-4">
    <v-app-bar class="bg-grey">
      <v-app-bar-title class="text-center">
        NOTICIAS
      </v-app-bar-title>
    </v-app-bar>
    <v-main>
      <v-container class="bg-grey-darken-1">
        <ul>
          <template v-for="dado in dados.items" >
            <v-card class="bg-grey-darken-3 ma-5">
              <v-card-title>{{ dado.titulo }} </v-card-title>
              <v-card-subtitle>{{ dado.data_pulblicacao }}</v-card-subtitle>
              <v-card-text>{{ dado.introducao }}</v-card-text>
              <v-card-actions class="border border-white">
                <v-btn :href="dado.link" target="_blank">
                  Ir para a notícia
                </v-btn>
              </v-card-actions>
            </v-card>
          </template>
        </ul>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>


const dados = ref({ items: [] });

async function recebe() {  
  const response = await fetch(`http://servicodados.ibge.gov.br/api/v3/noticias/`);
  const valores = await response.json();
  dados.value = valores;
}
onMounted(async () => {
  await recebe();
  console.log(dados.items);
});
</script>