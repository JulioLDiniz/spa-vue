<template>
	<button class="botao" :class="estiloDoBotao" @click="mandarParaOPai()" :tipo="tipo">{{ rotulo }}</button>	
</template>
<script>
export default{
	props: ['tipo','rotulo','confirmacao','estilo'],

	methods:{
		mandarParaOPai(){
			if(this.confirmacao){
				if(confirm('Deseja realmente excluir?')){
					this.$emit('botaoAtivado');
				}	
				return;
			}
			this.$emit('botaoAtivado');
		}
	},

	computed:{
		estiloDoBotao(){
			if(this.estilo === 'padrao' || !this.estilo) return 'botao-padrao';
			if(this.estilo === 'remover') return 'botao-perigo';
		}
	}
}
</script>
<style scoped>
.botao {
	display: inline-block;
	padding: 10px;
	border-radius: 3px;
	margin: 10px;
	font-size: 1.2em;
}

.botao-perigo {
	background: firebrick;
	color: white;
}

.botao-padrao {
	background: darkcyan;
	color: white;
}
</style>