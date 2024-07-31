<template>
    <div class="paciente-form">
      <h2>Cadastro de Paciente</h2>
      <form @submit.prevent="savePaciente">
        <div class="form-group">
          <label for="nome">Nome</label>
          <input type="text" id="nome" v-model="paciente.nome" required />
        </div>
        <div class="form-group">
          <label for="cpf">CPF</label>
          <input type="text" id="cpf" v-model="paciente.cpf" required />
        </div>
        <div class="form-group">
          <label for="telefone">Telefone</label>
          <input type="text" id="telefone" v-model="paciente.telefone" required />
        </div>
        <div class="form-group">
          <label for="rg">RG</label>
          <input type="text" id="rg" v-model="paciente.rg" required />
        </div>
        <div class="form-group">
          <label for="planoSaude">Plano de Saúde</label>
          <input type="text" id="planoSaude" v-model="paciente.planoSaude" required />
        </div>
        <div class="form-group">
          <label for="endereco">Endereço</label>
          <input type="text" id="endereco" v-model="paciente.endereco" required />
        </div>
        <button type="submit">Salvar</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        paciente: {
          nome: '',
          cpf: '',
          telefone: '',
          rg: '',
          planoSaude: '',
          endereco: ''
        }
      };
    },
    methods: {
      savePaciente() {
        console.log('Paciente salvo:', this.paciente);
      }
    }
  };
  </script>
  
  <style scoped>
  .paciente-form {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
  }
  
  button {
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  </style>
  