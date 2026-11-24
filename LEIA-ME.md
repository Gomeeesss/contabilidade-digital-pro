# Contabilidade Digital Pro — Portal Acadêmico (com banco de dados)

- `index.html` — o site completo (um único arquivo).
- Banco de dados: Supabase, projeto **contabilidade-digital-pro** (região São Paulo).

## Como funciona
- O login é conferido no banco (senhas guardadas criptografadas, nada de senha no código do site).
- Cada alteração é salva automaticamente no banco ~1 segundo depois (indicador "Salvo no banco" no topo).
- O aluno entra de qualquer computador/celular e encontra as atividades dele.
- A sessão dura 30 dias (não precisa logar de novo ao recarregar a página).
- Dados antigos que estavam só no navegador são enviados ao banco no primeiro login.
- Botão de chave 🔑: aluno troca a própria senha.
- Painel da Professora: lista a turma vinda do banco, último salvamento, nº de lançamentos e "Redefinir" senha.

## Tabelas (schema public)
- `portal_users` — login, senha (hash bcrypt), nome, papel (teacher/student)
- `portal_sessions` — tokens de sessão
- `portal_data` — empresas/lançamentos de cada usuário (JSON)

Acesso direto às tabelas é bloqueado (RLS); o site usa só as funções `portal_*`.

## Adicionar um aluno novo (SQL Editor do Supabase)
```sql
insert into public.portal_users(login, password_hash, senha_inicial, name, role)
values ('nome.sobrenome', extensions.crypt('senha123', extensions.gen_salt('bf')), 'senha123', 'NOME COMPLETO', 'student');
```

## Publicar na internet
Qualquer hospedagem de site estático serve (Netlify Drop, GitHub Pages, Vercel):
basta enviar o `index.html`.
