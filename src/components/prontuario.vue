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
  
      <div v-if="pacienteSalvo">
        <h2>Perfil do Paciente</h2>
        <p><strong>Nome:</strong> {{ paciente.nome }}</p>
        <p><strong>CPF:</strong> {{ paciente.cpf }}</p>
        <p><strong>Telefone:</strong> {{ paciente.telefone }}</p>
        <p><strong>RG:</strong> {{ paciente.rg }}</p>
        <p><strong>Plano de Saúde:</strong> {{ paciente.planoSaude }}</p>
        <p><strong>Endereço:</strong> {{ paciente.endereco }}</p>
        <button @click="editPaciente">Editar</button>
        <button @click="exportToPDF">Exportar para PDF</button>
      </div>
    </div>
  </template>
  
  <script>
  import jsPDF from "jspdf";
  
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
        },
        pacienteSalvo: false
      };
    },
    methods: {
      savePaciente() {
        this.pacienteSalvo = true;
        console.log('Paciente salvo:', this.paciente);
      },
      editPaciente() {
        this.pacienteSalvo = false;
      },
      exportToPDF() {
        const doc = new jsPDF();
        doc.text(`Nome: ${this.paciente.nome}`, 10, 10);
        doc.text(`CPF: ${this.paciente.cpf}`, 10, 20);
        doc.text(`Telefone: ${this.paciente.telefone}`, 10, 30);
        doc.text(`RG: ${this.paciente.rg}`, 10, 40);
        doc.text(`Plano de Saúde: ${this.paciente.planoSaude}`, 10, 50);
        doc.text(`Endereço: ${this.paciente.endereco}`, 10, 60);

        const fileName = `paciente_${this.paciente.nome.replace(/[^a-zA-Z0-9 ]/g, '')}.pdf`;

        doc.save(fileName);
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
    margin-bottom: 10px;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  button + button {
    margin-top: 10px;
  }
  </style>
  