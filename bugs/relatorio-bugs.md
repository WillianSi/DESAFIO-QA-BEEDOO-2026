# 7. Relatório de Bugs Encontrados

Os defeitos identificados durante os testes foram catalogados abaixo, priorizados de acordo com o impacto no negócio e na experiência do usuário.

---

## BUG-001 — Vulnerabilidade de Segurança (Stored XSS)

**Título do bug:**  
Execução de script malicioso via campo "Nome do curso" (Stored XSS).

**Passos para reproduzir:**

1. Acessar a página de cadastro de curso.
2. Inserir o payload <img src="x" onerror="alert('Bug!')"> no campo **Nome do curso**.
3. Preencher os demais campos e clicar em **Cadastrar curso**.
4. Acessar a página **Lista de cursos**.

**Resultado atual:**  
O sistema salva a entrada sem nenhum tratamento ou sanitização. Ao renderizar a listagem, o navegador interpreta a tag e executa o script JavaScript injetado.

**Resultado esperado:**  
O sistema deve sanitizar as entradas de texto (escapar tags HTML) e exibi-las apenas como texto comum.

**Severidade / Impacto:**  
Crítica — Permite roubo de sessão e injeção de código na máquina de outros usuários.

---

## BUG-002 — Falha Crítica de Funcionalidade (CRUD)

**Título do bug:**  
Falha na exclusão de cursos (Erro 405 Method Not Allowed).

**Passos para reproduzir:**

1. Cadastrar um curso válido.
2. Acessar a página **Lista de cursos**.
3. Clicar no botão vermelho **Excluir curso** em qualquer card.

**Resultado atual:**  
O curso não é removido da lista, ocorrendo uma falha silenciosa na interface. A requisição DELETE retorna erro **405 Method Not Allowed** no console/Network.

**Resultado esperado:**  
O curso deve ser excluído com sucesso da listagem e do banco de dados local, exibindo feedback visual para o usuário confirmando a ação.

**Severidade / Impacto:**  
Alta — Quebra de fluxo principal e acúmulo de dados indesejados.

---

## BUG-003 — Falha de Validação de Formulário

**Título do bug:**  
Ausência total de validação de obrigatoriedade nos campos de cadastro.

**Passos para reproduzir:**

1. Acessar a página de cadastro.
2. Deixar o formulário totalmente em branco ou omitir campos essenciais como Nome, Descrição e Tipo de Curso.
3. Clicar em **Cadastrar curso**.

**Resultado atual:**  
O sistema permite cadastro sem informações, gerando objetos vazios ou incompletos e exibindo cards em branco na listagem.

**Resultado esperado:**  
O sistema deve bloquear a submissão, destacando os campos obrigatórios e exibindo mensagens de validação.

**Severidade / Impacto:**  
Alta — Compromete a integridade da base de dados e a exibição do layout.

---

## BUG-004 — Injeção Visual e Falha de Validação de URL

**Título do bug:**  
Aceitação de payload embutido (Data URI/SVG) no campo de imagem.

**Passos para reproduzir:**

1. Acessar a página de cadastro.
2. Inserir o payload no campo **URL da imagem**.
   **Payload utilizado no teste:**
   ```
   data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg"><script>alert('Bomba SVG!')</script><text x="20" y="20">Imagem Infectada</text></svg>
   ```
4. Preencher os demais campos e clicar em **Cadastrar curso**.
5. Acessar a página **Lista de cursos**.

**Resultado atual:**  
O sistema não valida se o texto é um link válido (HTTP/HTTPS). Ele aceita a injeção do Data URI e renderiza a imagem SVG forjada no card.

**Resultado esperado:**  
O campo deve aplicar validação de formato que exija protocolos web válidos e rejeite arquivos embutidos ou links malformados.

**Severidade / Impacto:**  
Alta — Vulnerabilidade visual e falha na validação de dados.

---

## BUG-005 — Falha Crítica de Roteamento

**Título do bug:**  
Erro 404 ao recarregar rotas internas da aplicação.

**Passos para reproduzir:**

1. Acessar a aplicação e navegar até a página **Cadastro de curso**.
2. Começar a preencher o formulário.
3. Pressionar **F5** ou recarregar a página no navegador.

**Resultado atual:**  
A aplicação quebra e o servidor do Netlify retorna a página **404 Page Not Found**.

**Resultado esperado:**  
A página deve recarregar corretamente na mesma rota, sendo gerenciada pelo **Vue Router**.

**Severidade / Impacto:**  
Alta — Quebra total da experiência do usuário.

---

## BUG-006 — Inconsistência de Regras de Negócio

**Título do bug:**  
Aceitação de datas invertidas e valores numéricos negativos.

**Passos para reproduzir:**

1. Acessar a página de cadastro.
2. Inserir um número negativo no campo **Número de vagas** (ex: -5).
3. Inserir uma **Data de início** posterior à **Data de fim**.
4. Preencher os demais campos e cadastrar o curso.

**Resultado atual:**  
O sistema aceita datas inconsistentes e valores negativos.

**Resultado esperado:**  
O sistema deve validar regras de negócio e impedir esses valores.

**Severidade / Impacto:**  
Média — Afeta a credibilidade do sistema e a lógica de negócio.

---

## BUG-007 — Quebra de Layout em Dispositivos Móveis

**Título do bug:**  
Sobreposição e overflow no header em telas pequenas.

**Passos para reproduzir:**

1. Acessar a aplicação.
2. Abrir o **DevTools (F12)**.
3. Ativar a simulação de dispositivo móvel.
4. Selecionar uma tela estreita (ex: 280px).

**Resultado atual:**  
Os elementos do cabeçalho não se adaptam ao tamanho da tela, causando sobreposição e vazamento do layout.

**Resultado esperado:**  
A interface deve ser responsiva e adaptar os elementos adequadamente em qualquer resolução.

**Severidade / Impacto:**  
Baixa — Afeta a usabilidade em dispositivos móveis.

---

## BUG-008 — Má Experiência de Carregamento (Performance / UX)

**Título do bug:**  
Tela branca durante carregamento da lista em conexões lentas.

**Passos para reproduzir:**

1. Acessar a aplicação e abrir o **DevTools**.
2. Ir para a aba **Network**.
3. Alterar o throttling para **Slow 3G**.
4. Recarregar a página **Lista de cursos**.

**Resultado atual:**  
A tela permanece totalmente em branco até o carregamento terminar.

**Resultado esperado:**  
A aplicação deve exibir **spinner de carregamento ou skeleton screen** indicando que os dados estão sendo carregados.

**Severidade / Impacto:**  
Baixa — Problema de UX, não impede o uso funcional.
