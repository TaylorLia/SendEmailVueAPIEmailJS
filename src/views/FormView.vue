<style scoped>
@import './FormView.css';
</style>

<template>

<div class="center-container">
  <form ref="form" @submit.prevent="sendEmail" class="center-form">
    <div class="form-group">
      <li>
        <label for="nome">Nome</label>
      </li>
      <li>
        <input class="input-text" name="name" required minlength="2" :maxlength="50" />
      </li>
    </div>

    <div class="form-group">
      <li>
        <label for="email">Email</label>
      </li>
      <li>
        <input class="input-text" name="mail" type="email" minlength="7" required :maxlength="80" />
      </li>
    </div>

    <div class="form-group">
      <li>
        <label for="telefone">Telefone</label>
      </li>
      <li>
        <input class="input-text" name="phone" pattern="[0-9]*" minlength="8" required :maxlength="15" />
      </li>
    </div>

    <div class="form-group">
        <li>
          <label for="assunto">Assunto</label>
        </li>
        <li>
          <select class="input-text" placeholder="Selecione o assunto" name="subject" required>
            <option value="" disabled selected>Selecione o assunto</option>
            <option value="duvidas">Dúvidas sobre Serviços</option>
            <option value="elogios">Elogios</option>
            <option value="reclamacoes">Reclamações</option>
            <option value="outros">Outros</option>
          </select>
        </li>          
      </div>

    <div class="form-group">
        <li>
          <label for="descricao">Descrição</label>
        </li>
        <li>
          <textarea class="input-text text-description" name="message" required minlength="5" :maxlength="3000"></textarea>  
        </li>
      </div>

    <input type="submit" value="Enviar" class="button">
    <p v-if="emailSent" class="success-message">Seu email foi enviado com sucesso!</p>
    <p v-if="emailError" class="error-message">Ocorreu um erro ao enviar seu email. Tente novamente mais tarde.</p>
  </form>
</div>
</template>

<script>
import emailjs from '@emailjs/browser';

export default {
  data() {
    return {
      emailSent: false,
      emailError: false,
    };
  },
  methods: {
    sendEmail() {
      emailjs.sendForm('service_ein8w5p', 'template_b6zvy5t', this.$refs.form, 'bCp1ShaQ8HKouB7s1')
      .then((result) => {
          console.log('SUCCESS!', result.text);
          this.$refs.form.reset(); 
          this.emailSent = true;
          this.emailError = false;   
        })
        .catch((error) => {
          console.log('FAILED...', error.text);
          this.emailSent = false;
          this.emailError = true;
        });
    }
  }
}
</script>