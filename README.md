let questions = document.querySelectorAll('.css-10k9c7k'); 
let dataToSolve = []; 

questions.forEach(question => { 
    let question_id = question.id; 
    
    // Tratamento de erro caso o seletor mude 
    let headEl = question.querySelector('.css-1cwyvh6'); 
    let question_text = headEl ? headEl.firstChild.textContent : "Pergunta sem texto"; 
    
    let options = []; 
    let answers = question.querySelectorAll('button [data-testid="question-typography"]'); 
    
    answers.forEach((answer, index) => { 
        let letter = String.fromCharCode(65 + index); 
        options.push(`${letter}) ${answer.textContent}`);  // ✅ CORRIGIDO
    }); 
    
    dataToSolve.push({ 
        id: question_id, 
        pergunta: question_text, 
        alternativas: options 
    }); 
}); 

// Criação do Prompt
let promptText = `
Atue como um especialista no assunto dessas questões. 
Analise cada pergunta abaixo no formato JSON e identifique a alternativa correta. 

Para cada questão, retorne um objeto JSON contendo: 
1. "id": o ID da questão. 
2. "letra": apenas a letra da alternativa correta (A, B, C, D ou E). 

Formato de saída desejado (exemplo): 
[
    { "id": "1", "letra": "B" }, 
    { "id": "2", "letra": "A" }
]

Não inclua explicações, apenas o JSON puro.

DADOS: 
${JSON.stringify(dataToSolve, null, 2)}
`; 

copy(promptText); 
console.log("✅ Prompt copiado com letras! Agora vá ao Gemini/ChatGPT e dê Ctrl+V."); 
console.log("Preview do início do prompt:"); 
console.log(promptText.substring(0, 300) + "...");