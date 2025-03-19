1. Tabela de Usuários (users.csv)
// Gerar CSV para tabela de usuários
const fs = require('fs');
const { operadores, supervisor, matriculaParaAvaya } = require('./auth-data');

// Função para criar CSV
function generateUsersCSV() {
  // Cabeçalho
  let csv = 'id,fullName,birthDate,profileImage,bio,phone,email,address,type,matricula,avaya,lastSeen,isOnline\n';
  
  // Adicionar supervisor
  csv += `${supervisor.login},${supervisor.nome},,/placeholder.svg?height=200&width=200,Supervisor da equipe Hapvida,,,supervisor,,,${new Date().toISOString()},true\n`;
  
  // Adicionar operadores
  Object.entries(operadores).forEach(([avaya, dados]) => {
    const matricula = dados.matricula;
    csv += `${matricula},${dados.operador},,/placeholder.svg?height=200&width=200,Operador da equipe Hapvida,,,operador,${matricula},${avaya},${new Date().toISOString()},false\n`;
  });
  
  return csv;
}

// Gerar e salvar o CSV
const usersCSV = generateUsersCSV();
console.log(usersCSV);
