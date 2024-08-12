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
  
        <!-- Prontuário Digital -->
        <h3>Prontuário Digital</h3>
        <div class="form-group">
          <label for="tipoSanguineo">Tipo Sanguíneo</label>
          <input type="text" id="tipoSanguineo" v-model="prontuario.tipoSanguineo" required />
        </div>
        <div class="form-group">
          <label for="alergias">Alergias</label>
          <input type="text" id="alergias" v-model="prontuario.alergias" />
        </div>
        <div class="form-group">
          <label for="doencaCronica">Possui Doença Crônica?</label>
          <input type="checkbox" id="doencaCronica" v-model="prontuario.doencaCronica" />
        </div>
        <div v-if="prontuario.doencaCronica" class="form-group">
          <label for="qualDoenca">Qual Doença?</label>
          <input type="text" id="qualDoenca" v-model="prontuario.qualDoenca" />
        </div>
        <div class="form-group">
          <label for="usoMedicamento">Faz Uso Contínuo de Medicamento?</label>
          <input type="checkbox" id="usoMedicamento" v-model="prontuario.usoMedicamento" />
        </div>
        <div v-if="prontuario.usoMedicamento" class="form-group">
          <label for="qualMedicamento">Qual Medicamento?</label>
          <input type="text" id="qualMedicamento" v-model="prontuario.qualMedicamento" />
        </div>
        <div class="form-group">
          <label for="historicoDoencas">Histórico de Doenças</label>
          <textarea id="historicoDoencas" v-model="prontuario.historicoDoencas"></textarea>
        </div>
        <div class="form-group">
          <label for="historicoMedicamentos">Histórico de Medicamentos</label>
          <textarea id="historicoMedicamentos" v-model="prontuario.historicoMedicamentos"></textarea>
        </div>
        <div class="form-group">
          <label for="exames">Exames</label>
          <input type="file" id="exames" @change="handleFileUpload" />
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
  
        <!-- Exibindo informações do prontuário -->
        <h3>Prontuário Digital</h3>
        <p><strong>Tipo Sanguíneo:</strong> {{ prontuario.tipoSanguineo }}</p>
        <p><strong>Alergias:</strong> {{ prontuario.alergias }}</p>
        <p><strong>Possui Doença Crônica:</strong> {{ prontuario.doencaCronica ? 'Sim' : 'Não' }}</p>
        <p v-if="prontuario.doencaCronica"><strong>Qual Doença:</strong> {{ prontuario.qualDoenca }}</p>
        <p><strong>Uso Contínuo de Medicamento:</strong> {{ prontuario.usoMedicamento ? 'Sim' : 'Não' }}</p>
        <p v-if="prontuario.usoMedicamento"><strong>Qual Medicamento:</strong> {{ prontuario.qualMedicamento }}</p>
        <p><strong>Histórico de Doenças:</strong> {{ prontuario.historicoDoencas }}</p>
        <p><strong>Histórico de Medicamentos:</strong> {{ prontuario.historicoMedicamentos }}</p>
        <p><strong>Exames:</strong> <a :href="prontuario.examesUrl" download>Download</a></p>
  
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
          nome: "",
          cpf: "",
          telefone: "",
          rg: "",
          planoSaude: "",
          endereco: "",
        },
        prontuario: {
          tipoSanguineo: "",
          alergias: "",
          doencaCronica: false,
          qualDoenca: "",
          usoMedicamento: false,
          qualMedicamento: "",
          historicoDoencas: "",
          historicoMedicamentos: "",
          examesUrl: "",
        },
        pacienteSalvo: false,
      };
    },
    methods: {
      savePaciente() {
        this.pacienteSalvo = true;
        console.log("Paciente salvo:", this.paciente, this.prontuario);
      },
      editPaciente() {
        this.pacienteSalvo = false;
      },
      handleFileUpload(event) {
        const file = event.target.files[0];
        if (file) {
          this.prontuario.examesUrl = URL.createObjectURL(file);
        }
      },
      exportToPDF() {
        const doc = new jsPDF();
        doc.text(`Nome: ${this.paciente.nome}`, 10, 10);
        doc.text(`CPF: ${this.paciente.cpf}`, 10, 20);
        doc.text(`Telefone: ${this.paciente.telefone}`, 10, 30);
        doc.text(`RG: ${this.paciente.rg}`, 10, 40);
        doc.text(`Plano de Saúde: ${this.paciente.planoSaude}`, 10, 50);
        doc.text(`Endereço: ${this.paciente.endereco}`, 10, 60);
        doc.text(`Tipo Sanguíneo: ${this.prontuario.tipoSanguineo}`, 10, 70);
        doc.text(`Alergias: ${this.prontuario.alergias}`, 10, 80);
        doc.text(
          `Possui Doença Crônica: ${this.prontuario.doencaCronica ? "Sim" : "Não"}`,
          10, 90
        );
        if (this.prontuario.doencaCronica) {
          doc.text(`Qual Doença: ${this.prontuario.qualDoenca}`, 10, 100);
        }
        doc.text(
          `Uso Contínuo de Medicamento: ${this.prontuario.usoMedicamento ? "Sim" : "Não"}`,
          10, 110
        );
        if (this.prontuario.usoMedicamento) {
          doc.text(`Qual Medicamento: ${this.prontuario.qualMedicamento}`, 10, 120);
        }
        doc.text(`Histórico de Doenças: ${this.prontuario.historicoDoencas}`, 10, 130);
        doc.text(`Histórico de Medicamentos: ${this.prontuario.historicoMedicamentos}`, 10, 140);
        doc.save(`${this.paciente.nome}_prontuario.pdf`);
      },
    },
  };
  </script>
  
<style scoped>
  @keyframes gradientBG {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  .paciente-form {
    max-width: 100%;
    background: rgba(255, 255, 255, 0.219);
    backdrop-filter: blur(10px);
    padding: 30px;
    border-radius: 15px;
    box-shadow: 0 4px 30px rgb(0, 0, 0);
    border: 1px solid rgb(255, 255, 255);
    margin: 20px;
  }
  
  .form-group {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .form-group label {
    width: 30%;
    margin-right: 10px;
    font-weight: bold;
    font-size: 20px;
    color: #000000;
  }
  
  .form-group input,
  .form-group textarea {
    width: 70%;
    padding: 12px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-sizing: border-box;
    font-size: 14px;
  }
  
  .form-group.full-width input,
  .form-group.full-width textarea {
    width: 100%;
  }
  
  .form-group input[type="text"],
  .form-group textarea {
    background-color: #f9f9f9;
    border: 1px solid #ddd;
  }
  
  .form-group input:focus,
  .form-group textarea:focus {
    border-color: #007bff;
  }
  
  button {
    width: 100%;
    padding: 15px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin-top: 20px;
    font-weight: bold;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  button + button {
    margin-top: 10px;
  }
</style>
  