//O principal objetivo deste desafio é fortalecer suas habilidades em lógica de programação. Aqui você deverá desenvolver a lógica para resolver o problema.


// Variáveis globais
let nomeAmigos = []; // Array que armazena a lista de nomes dos participantes
let amigos = document.querySelector('#amigo'); // Input para digitar os nomes
let listaAmigos = document.querySelector('#listaAmigos'); // Lista UL onde os nomes são exibidos
let resultado = document.querySelector('#resultado'); // Elemento para mostrar o resultado do sorteio

// Função que atualiza a lista de amigos na interface
function atualizarListaAmigos() {
    let html = '';
    // Constrói cada item da lista com nome e botão de remover
    for (let i = 0; i < nomeAmigos.length; i++) {
        html += `
            <li>
                ${nomeAmigos[i]} 
                <button 
                    onclick="removerAmigo(${i})" 
                    style="
                        font-size: 10px; 
                        padding: 1px 4px; 
                        margin-left: 8px;
                        border: none;
                        border-radius: 3px;
                        background: #ff4444;
                        color: white;
                        cursor: pointer;
                    "
                >
                    X
                </button>
            </li>`;
    }
    listaAmigos.innerHTML = html; // Atualiza o conteúdo da lista
}

// Função para adicionar novo amigo à lista
const adicionarAmigo = () => {
    // Validação de campo vazio
    if (amigos.value === '') {
        alert("Por favor, insira um nome.");
    } else {
        nomeAmigos.push(amigos.value); // Adiciona ao array
        atualizarListaAmigos(); // Atualiza a lista na interface
    }
    limparNomeAmigo(); // Limpa o campo de input
}

// Função para limpar o campo de digitação
const limparNomeAmigo = () => {
    amigos.value = ''; // Reseta o valor do input
}

// Função para remover um amigo da lista
function removerAmigo(index) {
    nomeAmigos.splice(index, 1); // Remove o elemento do array
    atualizarListaAmigos(); // Atualiza a lista na interface
}

// Função principal que realiza o sorteio
function sortearAmigo() {
    if (nomeAmigos.length === 0 || nomeAmigos.length === 1) {
        resultado.innerHTML = '';
        return;
    }
    let sorteado = nomeAmigos[Math.floor(Math.random() * nomeAmigos.length)];
    resultado.innerHTML = `<p style="color: black;">Amigo Sorteado:</p><li>${sorteado}</li>`;
    
    // Mostrar botão de reinício
    document.querySelector('#botaoReiniciar').classList.remove('hidden');
    document.querySelector('.button-container').style.display = 'flex';
}

// Função para reiniciar o sistema
function reiniciarSistema() {
    if (confirm("Deseja reiniciar?")) {
        // Reinicia o array de nomes
        nomeAmigos = [];
        
        // Limpa a lista visual
        atualizarListaAmigos();
        
        // Limpa o resultado do sorteio
        resultado.innerHTML = '';
        
        // Limpa o input
        limparNomeAmigo();
        
        // Enfocar o input automaticamente
        amigos.focus();
    }

    // Ocultar botão de reinício
    document.querySelector('#botaoReiniciar').classList.add('hidden');
}
