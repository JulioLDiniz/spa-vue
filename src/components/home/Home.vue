<template>
  <div >
    <h1 class="centralizado">Alura pic</h1>
    <input type="text" class="filtro" v-on:input="filtro = $event.target.value" placeholder="Filtre por qualquer coisa">
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :src="foto.url" :titulo="foto.titulo"/>
          <botao-deletar tipo="button" @botaoAtivado="remover(foto)" rotulo="Remover" :confirmacao="true"  estilo="remover"/>
        </meu-painel>        
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue';
export default {

  components:{
    'meu-painel' : Painel,
    'imagem-responsiva' : ImagemResponsiva,
    'botao-deletar' : Botao
  },

  methods: {
    remover(foto){
      alert(foto.titulo+' Removido com sucesso!');
    }
    
  },

  data(){
    return {
      fotos: [],
      filtro:''
    }
  },

  computed:{
    fotosComFiltro(){
      if(this.filtro){
        let exp = new RegExp(this.filtro.trim(),'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      }else{
        return this.fotos;
      }
    }
  },

  created() {

    this.$http.get('http://localhost:3000/v1/fotos')
    .then(res => res.json())
    .then(fotos => this.fotos = fotos);
  }
}
</script>

<style>
.centralizado{
  text-align: center;
}
.lista-fotos{
  list-style: none;
}
.lista-fotos-item{
  display: inline-block;
}
.filtro{
  display: block;
  width: 100%;
}
</style>
