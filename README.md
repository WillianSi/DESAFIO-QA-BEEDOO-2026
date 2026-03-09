# DESAFIO QA BEEDOO 2026

## 1. Análise da Aplicação

A aplicação analisada consiste em um sistema web simples de cadastro e listagem de cursos.

O objetivo principal da aplicação é permitir que usuários registrem cursos através de um formulário e posteriormente visualizem esses cursos em uma lista organizada em formato de cards.

Trata-se de uma aplicação front-end que simula um sistema CRUD parcial, focado em três operações principais:

- Cadastro de cursos
- Visualização dos cursos cadastrados
- Exclusão de cursos

### Componentes identificados

Durante a exploração da aplicação foram identificados os seguintes componentes principais:

- Página de cadastro de cursos
- Formulário de cadastro contendo múltiplos campos
- Página de listagem de cursos
- Cards de exibição de cursos
- Botão de exclusão de cursos

### Campos disponíveis no formulário de cadastro

O formulário apresenta os seguintes campos:

- Nome do curso
- Descrição do curso
- Instrutor
- URL da imagem de capa
- Data de início
- Data de fim
- Número de vagas
- Tipo de curso ("Presencial" ou "Online")
- Endereço (Campo condicional: Presencial)
- Link de inscrição (Campo condicional: Online)

### Tecnologias e características observadas

Com base na interface, no comportamento da aplicação e com a utilização da extensão Wappalyzer, foi possível observar que trata-se de uma aplicação web front-end hospedada na plataforma Netlify (atuando como PaaS e CDN). O desenvolvimento e a componentização da interface foram construídos utilizando os frameworks JavaScript Vue.js e Quasar.

Em relação à arquitetura de dados, a aplicação não consome um banco de dados real centralizado. A persistência das informações cadastradas é feita localmente no lado do cliente (Front-end), utilizando o Local Storage do navegador (na chave @beedoo-qa-tests/courses) para simular o armazenamento e a listagem dos cursos.

---

## 2. Principais fluxos da aplicação

Durante a exploração da aplicação foram identificados os seguintes fluxos principais:

1. Cadastro de curso
2. Visualização da lista de cursos
3. Exclusão de cursos
4. Navegação entre as páginas da aplicação

### Fluxo principal esperado:

Usuário acessa a aplicação →  
Preenche o formulário de cadastro de curso →  
Clica no botão "Cadastrar curso" →  
O curso é registrado no sistema →  
O curso passa a aparecer na lista de cursos.

### Fluxo de visualização da lista de cursos

Usuário acessa a página "Listar cursos" →  
O sistema carrega os cursos cadastrados →  
Cada curso é exibido em formato de card contendo informações como nome, descrição, datas e número de vagas.

### Fluxo de exclusão de curso

Usuário acessa a lista de cursos →  
Seleciona a opção "Excluir curso" em um dos cards →  
O sistema remove o curso da lista exibida.

---

## 3. Pontos críticos para teste

Durante a análise da aplicação foram identificados alguns pontos que merecem atenção especial durante a execução dos testes. Esses pontos estão relacionados principalmente à validação de dados, comportamento do sistema, integridade das informações exibidas e experiência do usuário.

### Validação de dados

- Validação dos campos do formulário de cadastro de cursos
- Validação do campo número de vagas para garantir que apenas valores numéricos válidos sejam aceitos
- Consistência entre data de início e data de fim do curso
- Validação do formato da URL da imagem de capa
- Validação do campo **Link de inscrição**, exibido apenas quando o tipo de curso é **Online** (campo condicional)

### Comportamento funcional do sistema

- Persistência do curso cadastrado na lista de cursos
- Atualização correta da listagem após a criação ou exclusão de cursos
- Funcionamento adequado da funcionalidade de exclusão de cursos
- Comportamento do sistema ao receber dados inválidos ou inconsistentes

### Interface e experiência do usuário

- Comportamento da interface e dos componentes em diferentes tamanhos de tela (responsividade)
- Clareza e organização visual das informações exibidas nos cards de cursos
- Consistência do layout e alinhamento dos elementos da interface
- Feedback visual adequado após ações do usuário, como cadastro ou exclusão de cursos
- Facilidade de navegação entre as páginas da aplicação
- Exibição correta de mensagens de erro ou validação nos campos do formulário

### Segurança

- Sanitização de inputs nos campos de texto, prevenindo possíveis injeções de scripts maliciosos (como ataques XSS).
- Validação de dados inseridos pelo usuário para evitar a execução de conteúdos não seguros na interface.
- Verificação da segurança de links inseridos pelo usuário, como o campo de URL da imagem ou link de inscrição.
- Garantia de que dados inseridos pelo usuário sejam exibidos de forma segura na interface, sem permitir execução de código.

## 4. Estratégia de testes

A estratégia de testes foi definida com base na análise das funcionalidades disponíveis na aplicação, com o objetivo de validar tanto o funcionamento correto do sistema quanto possíveis comportamentos inesperados.

Os testes foram planejados considerando diferentes tipos de cenários, buscando garantir uma cobertura adequada das funcionalidades principais do sistema.

Foram considerados os seguintes tipos de testes:

- **Cenários positivos:** validação do funcionamento esperado da aplicação, como o cadastro correto de um curso e sua exibição na lista.
  
- **Cenários negativos:** tentativa de executar ações com dados inválidos ou incompletos, verificando se o sistema realiza as validações necessárias.

- **Validação de campos:** verificação das regras de preenchimento dos campos do formulário, como obrigatoriedade, formato de dados e tipos de entrada.

- **Testes de usabilidade:** análise da clareza da interface, facilidade de navegação entre as páginas e feedback visual apresentado ao usuário.

- **Testes de comportamento inesperado:** avaliação de como o sistema se comporta em situações não previstas, como inserção de valores extremos, dados inconsistentes ou entradas incomuns.

---

## 5. Casos de teste

Os cenários e casos de teste foram documentados na planilha:

Link da planilha:
https://docs.google.com/spreadsheets/d/1IQFzcgcPo8kF9CVAsVv4ItPC3KuPL50wuH7m6_vxldA/edit?usp=sharing

---

## 6. Evidências de testes

As evidências da execução dos testes estão disponíveis no link:

https://drive.google.com/drive/folders/14IFNZ_mZEhxwRH4oFnnaEQYZ7341evR4?usp=sharing

---

## 7. Relatório de bugs

Os bugs encontrados estão documentados abaixo:

[Relatório de Bugs](bugs/relatorio-bugs.md)

